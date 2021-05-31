<script>
  import Card from '$lib/Card.svelte'
  export let cards
</script>

<div class="grid">
  {#each cards as card, i}
    <Card icon={card} i={i} />
  {/each}
</div>

<style>
  .grid {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    gap: 1rem;
  }

  .cell {
    flex: 1 1 300px;
    height: 300px;
    display: grid;
  }
</style>