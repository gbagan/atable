<script lang="ts">
  import toast, {Toaster} from 'svelte-5-french-toast';
  import Input from "./components/Input.svelte";
  import Generator from "./components/Generator.svelte";
  import { tick } from "svelte";

  let names: { name: string, label: string }[] | null = $state.raw(null);
  let input = $state.raw("");

  async function run() {
    const res = [];
    const nameSet = new Set<string>();
    const labelSet = new Set<string>();
    const parsed = input.split('\n').map(s => s.trim()).filter(s => s.length > 0);
    try {
      if (parsed.length === 0) throw Error("Entrée vide");
      if (parsed.length > 18) throw Error("Limité à 18 personnes");
      for (const line of parsed) {
        const words = line.split(',').map(s => s.trim()).filter(s => s.length > 0);
        if (words.length !== 2) throw Error(`Ligne "${line}" invalide`);
        const [name, label] = words;
        if (label.length > 2) throw Error("Les labels doivent avoir au plus 2 caractères")
        if (nameSet.has(name)) throw Error(`Le prénom "${name}" apparait deux fois`);
        if (labelSet.has(label)) throw Error(`Le label "${label}" apparait deux fois`);
        nameSet.add(name);
        labelSet.add(label);
        res.push({ name, label });
      }
      names = res;
      await tick();
      window.print();
    } catch (e) {
      toast.error(`Erreur: ${(e as Error).message}`);
    }
  }

  function restart() {
    names = null;
  }
</script>

{#if names === null}
  <Input bind:input={input} {run} />
  <Toaster />
{:else}
  <Generator {names} {restart} />
{/if}
