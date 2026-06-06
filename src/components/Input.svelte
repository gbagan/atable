<script lang="ts">
  type Props = {
    input: string;
    run: () => void;
  }

  let { input = $bindable(), run }: Props = $props();
</script>

<textarea
  placeholder="Entrez les prénoms, un par ligne"
  bind:value={input}
  cols="20"
  rows="25"
></textarea>
<button class="ui-button" onclick={run}>Générer</button>

<style>
  textarea {
    display: block;
    padding: 0.625rem;
    font-size: 0.875rem;
    font-family: var(--mono);
    color: var(--text);
    background-color: var(--gray-50);
    border-radius: 0.5rem;
    border: 1px solid var(--gray-300);
  }

  textarea:focus {
    outline: 1px solid var(--blue-500);
    border-color: var(--blue-500);
  }
</style>