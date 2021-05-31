<script>
  import { onMount } from 'svelte';
  import Icon from 'svelte-awesome';

  export let icon
  export let i

  onMount(() => {
    const card = document.querySelector(`.card-${i}`);
    card.addEventListener( 'click', function() {
      card.classList.toggle('is-flipped');
    });
  })
  
</script>

<div class="scene scene--card">
  <div class={`card-${i} card is-flipped`}>
    <div class="card__face card__face--front"><Icon data={icon} scale="3" /></div>
    <div class="card__face card__face--back">back</div>
  </div>
</div>

<style>
  .scene {
    width: 300px;
    height: 300px;
    perspective: 600px;
  }

  .card {
    position: relative;
    width: 100%;
    height: 100%;
    cursor: pointer;
    transform-style: preserve-3d;
    transform-origin: center right;
    transition: transform 1s;
  }

  .card.is-flipped {
    transform: translateX(-100%) rotateY(-180deg);
  }

  .card__face {
    position: absolute;
    display: grid;
    place-items: center;
    width: 100%;
    height: 100%;
    backface-visibility: hidden;
  }

  .card__face--front {
    background: #eee;
  }

  .card__face--back {
    background: blue;
    transform: rotateY(180deg);
  }
</style>