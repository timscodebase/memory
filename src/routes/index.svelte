<script>
  import { onMount } from 'svelte';

  import Grid from '$lib/Grid.svelte'
  import {
    faPaw,
    faHippo,
    faDog,
    faSpider,
    faKiwiBird,
    faHorseHead,
    faHorse,
    faFrog,
    faFish,
    faDragon,
    faDove,
    faCrow,
    faCat
  } from '@fortawesome/free-solid-svg-icons';
  
  let started = false
  let numOfPairs = 1
  let iconArray = []
  let shuffledArray = []
  let cards
  let resetCards

  onMount(() => {
    resetCards = () => {
      cards = document.querySelectorAll(`.card`);
      cards.forEach(card => {
        if (!card.classList.contains('is-flipped')) {
          card.classList.add('is-flipped');
        }
      });
    }
  })

  const icons = [
    faPaw,
    faHippo,
    faDog,
    faSpider,
    faKiwiBird,
    faHorseHead,
    faHorse,
    faFrog,
    faFish,
    faDragon,
    faDove,
    faCrow,
    faCat
  ]

  function shuffle(array) {
    var currentIndex = array.length,  randomIndex;

    while (0 !== currentIndex) {
      randomIndex = Math.floor(Math.random() * currentIndex);
      currentIndex--;

      [array[currentIndex], array[randomIndex]] = [
        array[randomIndex], array[currentIndex]];
    }

    return array;
  }

  function createArray(numOfPairs) {
    iconArray = []
    const shuffledIcons = shuffle(icons)
    shuffledIcons.slice(0, numOfPairs).map(icon => iconArray.push(icon, icon))
    shuffledArray = shuffle(iconArray)
  }

  function increase() {
    if (numOfPairs < 8) {
      numOfPairs = numOfPairs + 1
    }
  }

  function decrease() {
    if (numOfPairs > 1) {
      numOfPairs = numOfPairs - 1
    }
  }
  
  function play() {
    started = true
    createArray(numOfPairs)
  }

  function reset() {
    started = false
    resetCards()
  }
</script>

<h1>My Remembery Game</h1>
<p>Find pairs to remove cards and <span>win!</span></p>

<div class="set-board">
  <button on:click={decrease}>-</button>
  <div>{numOfPairs}</div>
  <button on:click={increase}>+</button>
  <button on:click={started ? reset : play}>{started ? "Reset" : "Play"}</button>
</div>

<div class="main">
  <Grid cards={shuffledArray} />
</div>

<style>
  button {
    border: none;
    outline: none;
    user-select: none;
    background: transparent;
  }

  .set-board {
    width: 50%;
    margin: 2rem auto;
    display: flex;
    justify-content: space-between;
  }
</style>