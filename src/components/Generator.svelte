<script lang="ts">
  import { chunks, range } from "@gbagan/utils";
  import Fiche from "./Fiche.svelte";

  type Props = {
    names: { name: string, label: string }[];
    restart: () => void;
  }

  let { names, restart }: Props = $props();

  const graph = {
    layout:[{"x":0.5326952465213545,"y":0.41293332260918525},{"x":0.05592475669588997,"y":0.5766860371591732},{"x":0.3637899139387115,"y":0.23245596396686238},{"x":0.1659293814847583,"y":0.10407785731520952},{"x":0.8093782675138743,"y":0.061610230837287866},{"x":0.8762969516609025,"y":0.36917879835920536},{"x":0.6807287058634279,"y":0.5353494731762246},{"x":0.8582803828520872,"y":0.6561570015281911},{"x":0.5095310866243062,"y":0.7513874366605002},{"x":0.36025094506555133,"y":0.5815169307488136},{"x":0.047258304512185316,"y":0.29612221507279013},{"x":0.33579988739644495,"y":0.855626156197217},{"x":0.6832622858521676,"y":0.844044076248693},{"x":0.21734496903402237,"y":0.2966952867369098},{"x":0.6526381404327194,"y":0.22371913456124828},{"x":0.9552300329767555,"y":0.5092998471808896},{"x":0.23542186117590283,"y":0.5866645218370465},{"x":0.19616645218370465,"y":0.7317823534143006}],
    edges:[[1,0],[2,0],[6,0],[5,0],[2,1],[13,1],[10,1],[3,1],[14,2],[4,2],[3,2],[10,3],[13,3],[4,3],[5,4],[4,14],[7,5],[15,5],[6,5],[7,6],[8,6],[15,7],[12,7],[8,7],[9,8],[11,8],[16,9],[9,17],[17,16],[11,17],[12,8],[11,9],[9,0]]
  }

  function nbors(v: number) {
    const res = [];
    for (const [u, w] of graph.edges) {
      if (u === v && w < names.length) {
        res.push(w);
      } else if (w === v && u < names.length) {
        res.push(u);
      }
    }
    return res;
  }

  function enemies(v: number) {
    return nbors(v).map(u => names[u].name);
  }

</script>

<div class="notprinted">
  <button class="ui-button" onclick={restart}>Retour</button>
  <button class="ui-button" onclick={() => window.print()}>Imprimer</button>
  <ul>
    <li>Imprimez la page (Control + P)</li>
    <li>Activez l'impression des graphismes d'arrière-plan</li>
    <li>Désactivez l'impression d'entêtes et pieds de pages</li>
  </ul>
</div>


<div class="page">
  <div class="fiches2">
    {#each names as name, i}
      <div class="fiche2">
        <div class={["fiche2-title", {small: name.name.length > 9}]}>{name.name}</div>
        <div class="fiche2-rejected-list">
          {#each enemies(i) as enemy}
            <div class="fiche2-rejected">
              {enemy}
            </div>
          {/each}
        </div>
      </div>
    {/each}
  </div>
</div>

<div class="page">
  <div class="graph">
    <svg viewBox="0 0 1500 1000">
      {#each graph.edges as [u, v]}
        {#if u < names.length && v < names.length}
          {const p1 = $derived(graph.layout[u])}
          {const p2 = $derived(graph.layout[v])}
          <line
            x1={1500*p1.x}
            y1={1000*p1.y}
            x2={1500*p2.x}
            y2={1000*p2.y}
            stroke-width="5"
            stroke="black"
          />
        {/if}
      {/each}
      {#each names as name, i}
        {const {x, y} = $derived(graph.layout[i])}
        <circle
          cx={1500*x}
          cy={1000*y}
          r="50"
          fill="white"
          stroke-width="5"
          stroke="black"
        />
        <text
          x={1500*x}
          y={1000*y}
          text-anchor="middle"
          dominant-baseline="middle"
          font-size="40"
        >{name.label}</text>
      {/each}
    </svg>
  </div>
</div>

<div class="page">
  <div class="graph">
    <svg viewBox="0 0 1500 1000">
      {#each names as name, i}
        {const {x, y} = $derived(graph.layout[i])}
        <circle
          cx={1500*x}
          cy={1000*y}
          r="50"
          fill="white"
          stroke-width="5"
          stroke="black"
        />
        <text
          x={1500*x}
          y={1000*y}
          text-anchor="middle"
          dominant-baseline="middle"
          font-size="40"
        >{name.label}</text>
      {/each}
    </svg>
  </div>
</div>

{#each chunks(range(0, names.length), 4) as chk}
  <div class="page">
    <div class="fiches">
      {#each chk as i}
        <Fiche name={names[i].name} enemies={enemies(i)} />
      {/each}
    </div>
  </div>
{/each}

<style>
  @page {
    size: A4 landscape;
    margin: 0;
  }

  .page {
    display: none;
  }

  .notprinted ul {
    margin-top: 1rem;
    list-style-type: disc;
    padding-left: 1.5rem;
  }

  @media print {
    @page {
      size: A4 landscape;
      margin: 0;
    }

    .page {
      width: 297mm;
      height: 210mm;
      overflow: hidden;
      break-after: page;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .notprinted {
      display: none;
    }
  }

  .fiches2 {
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    gap: 0.5cm;
  }

  .fiche2 {
    display: flex;
    flex-direction: column;
    align-items: center;
    background: var(--stone-200);
    width: 4.2cm;
    height: 6cm;
    border-radius: 1cm;
    gap: 0.5cm;
  }

  .fiche2-title {
    font-size: 0.8cm;
    font-weight: bold;
    font-family: 'Shantell Sans', cursive;
    &.small {
      font-size: 0.5cm;
    }
  }

  .fiche2-rejected-list {
    display: flex;  
    flex-direction: column;
    align-items: center;
  }

  .fiche2-rejected {
    font-size: 0.6cm;
  }

  .graph {
    width: 27cm;
    height: 18cm;
  }


  .fiches {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 0.25cm;
  }
</style>