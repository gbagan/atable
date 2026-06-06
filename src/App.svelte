<script lang="ts">
  import Input from "./components/Input.svelte";
  import Generator from "./components/Generator.svelte";
  import { tick } from "svelte";

  let names: { name: string, label: string }[] | null = $state.raw(null);
  let input = $state.raw("")

  async function run() {
    const res = [];
    const parsed = input.split('\n').map(s => s.trim()).filter(s => s.length > 0);
    if (parsed.length === 0) return;
    for (const line of parsed) {
      const words = line.split(' ').map(s => s.trim()).filter(s => s.length > 0);
      if (words.length !== 2) return;
      res.push({ name: words[0], label: words[1] });
    }
    names = res;
    await tick();
    window.print();
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