<script lang="ts">
  type Props = {
    name: string;
    label: string;
    enemies: string[];
  }

  let { name, label, enemies }: Props = $props();
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
    <div class="family-name">Label {label}</div>
    <div class="page-num">18</div>
  </div>
</div>

<style>
  .spread {
    display: flex;
    gap: 8px;
    width: 20cm;
    width: 100%;
    margin-bottom: 0.5cm;
  }

  .card {
    background: white;
    border-radius: 16px;
    box-shadow: 0 2px 12px rgba(0,0,0,0.12);
    padding: 28px 20px;
    flex: 1;
    position: relative;
    min-height: 340px;
  }

  .card-left {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 24px;
  }

  .je-suis-label {
    font-family: cursive;
    font-size: 15px;
    color: #333;
    letter-spacing: 0.5px;
  }

  .oval-wrap {
    width: 180px;
    height: 80px;
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
        transparent 14px,
        rgba(255,255,255,0.55) 14px,
        rgba(255,255,255,0.55) 28px
      ),
      repeating-linear-gradient(
        90deg,
        transparent,
        transparent 14px,
        rgba(255,255,255,0.55) 14px,
        rgba(255,255,255,0.55) 28px
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
    font-size: 36px;
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
    padding: 14px 10px 14px 0;
  }

  .reject-label {
    writing-mode: vertical-rl;
    text-orientation: mixed;
    transform: rotate(180deg);
    font-size: 11px;
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
    font-size: 16px;
    color: #1a1a1a;
  }

  .card-right {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding-bottom: 40px;
  }

  .big-name {
    font-family: 'Shantell Sans', cursive;
    font-size: 64px;
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

  .family-name {
    font-family: 'Shantell Sans', cursive;
    font-size: 30px;
    color: #1a1a1a;
    letter-spacing: 2px;
  }

  .page-num {
    position: absolute;
    bottom: 14px;
    right: 16px;
    font-size: 13px;
    color: #bbb;
    border: 1.5px solid #ddd;
    border-radius: 6px;
    padding: 2px 8px;
    font-family: 'Shantell Sans', cursive;
  }
</style>