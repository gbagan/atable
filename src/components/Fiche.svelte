<script lang="ts">
  type Props = {
    name: string;
    enemies: string[];
  }

  let { name, enemies }: Props = $props();
</script>

<div class="spread">
  <div class="card card-left">
    <span class="je-suis-label">Je suis</span>

    <div class="oval-wrap">
      <div class="gingham-bg"></div>
      <div class="oval-name">{name}</div>
    </div>

    <div class="reject-block">
      <span class="reject-label">Je ne veux pas être avec</span>
      <div class="reject-names">
        {#each enemies as enemy}
          <span>{enemy}</span>
        {/each}
      </div>
    </div>
  </div>
  <div class="card card-right">
    <div class="big-name">{name}</div>
    <div class="underline-name"></div>
  </div>
</div>

<style>
  .spread {
    display: flex;
    gap: 0.25cm;
  }

  .card {
    background: white;
    border-radius: 16px;
    box-shadow: 0 2px 12px rgba(0,0,0,0.12);
    padding: 0.7cm 0.5cm;
    flex: 1;
    position: relative;
    height: 9.5cm;
  }

  .card-left {
    width: 7cm;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.6cm;
  }

  .je-suis-label {
    font-family: cursive;
    font-size: 0.375cm;
    color: #333;
    letter-spacing: 0.5px;
  }

  .oval-wrap {
    width: 4.9cm;
    height: 2.2cm;
    position: relative;
    border-radius: 50%;
    overflow: hidden;
  }

  .gingham-bg {
    position: absolute;
    inset: 0;
    background-color: #f5b8be;
    background-image:
      repeating-linear-gradient(
        0deg,
        transparent,
        transparent 0.35cm,
        rgba(255,255,255,0.55) 0.3cm,
        rgba(255,255,255,0.55) 0.7cm
      ),
      repeating-linear-gradient(
        90deg,
        transparent,
        transparent 0.35cm,
        rgba(255,255,255,0.55) 0.35cm,
        rgba(255,255,255,0.55) 0.7cm
      );
    border-radius: 50%;
  }

  .oval-name {
    position: absolute;
    inset: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'Shantell Sans', cursive;
    font-size: 0.9cm;
    color: #1a1a1a;
    letter-spacing: 1px;
  }

  .reject-block {
    display: flex;
    align-items: stretch;
    gap: 0;
    width: 100%;
    border: 1.5px dashed #e88;
    border-radius: 10px;
    padding: 0.35cm 0.25cm 0.35cm 0;
  }

  .reject-label {
    writing-mode: vertical-rl;
    text-orientation: mixed;
    transform: rotate(180deg);
    font-size: 0.3cm;
    color: #888;
    padding: 0 8px;
    letter-spacing: 0.5px;
    white-space: nowrap;
  }

  .reject-names {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2px;
  }

  .reject-names span {
    font-family: 'Shantell Sans', cursive;
    font-size: 0.45cm;
    color: #1a1a1a;
  }

  .card-right {
    width: 7cm;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding-bottom: 1cm;
  }

  .big-name {
    font-family: 'Shantell Sans', cursive;
    font-size: 1.1cm;
    color: #1a1a1a;
    line-height: 1;
    margin-bottom: 4px;
  }

  .underline-name {
    width: 90%;
    height: 2px;
    background: #1a1a1a;
    margin: 0 auto 10px auto;
  }
</style>