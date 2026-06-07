<script lang="ts">
  type Props = {
    input: string;
    run: () => void;
  }

  let { input = $bindable(), run }: Props = $props();
</script>

<div class="wrapper">
  <h1>Générateur de fiches pour A Table!</h1>

  <textarea
    placeholder="Entrez les prénoms et labels séparés par une virgule, un par ligne"
    bind:value={input}
    cols="40"
    rows="25"
  ></textarea>
  <button class="ui-button" onclick={run}>Générer</button>
</div>


<style>
  .wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
  }

  h1 {
    font-size: 1.75rem;
    font-weight: bold;
  }

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