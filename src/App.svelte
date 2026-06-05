<script lang="ts">
  import Input from "./components/Input.svelte";
  import Generator from "./components/Generator.svelte";

  let names: { name: string, label: string }[] | null = $state(null); 

  function run(input: string) {
    const res = [];
    const parsed = input.split('\n').map(s => s.trim()).filter(s => s.length > 0);
    if (parsed.length === 0) return;
    for (const line of parsed) {
      const words = line.split(' ').map(s => s.trim()).filter(s => s.length > 0);
      if (words.length !== 2) return;
      res.push({ name: words[0], label: words[1] });
    }
    names = res;
  }
</script>

{#if names === null}
  <Input {run} />
{:else}
  <Generator {names} />
{/if}