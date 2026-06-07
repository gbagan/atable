<script lang="ts">
  import toast, {Toaster} from 'svelte-5-french-toast';
  import Input from "./components/Input.svelte";
  import Generator from "./components/Generator.svelte";
  import { tick } from "svelte";

  let names: { name: string, label: string }[] | null = $state.raw(null);
  let input = $state.raw("")

  async function run() {
    const res = [];
    const parsed = input.split('\n').map(s => s.trim()).filter(s => s.length > 0);
    try {
      if (parsed.length === 0) throw Error("Entrée vide");
      for (const line of parsed) {
        const words = line.split(' ').map(s => s.trim()).filter(s => s.length > 0);
        if (words.length !== 2) throw Error(`Ligne "${line}" invalide"`);
        res.push({ name: words[0], label: words[1] });
      }
      if (res.length > 18) throw Error("Limité à 18 personnes");
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
{:else}
  <Generator {names} {restart }/>
{/if}
<Toaster/>