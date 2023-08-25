<script>
  import {onMount} from 'svelte';
	import { get } from 'svelte/store';

  let data = {};

  onMount(async () => {
    getData();
  });

  const getData = async () => {
    const row = await(await fetch('https://api.adviceslip.com/advice')).json();
    data = {
      id: row.slip.id,
      text: row.slip.advice
    }
  }
</script>

<style>
  * {
    font-family: Helvetica;
  }
  main {
    width: 40rem;
    height: 30rem;
    border-radius: 1rem;
    margin: 6rem auto;
    box-sizing: border-box;
    box-shadow: 0 0 4px #999;
    padding: 1rem;
    background-color: #333;
  }
  .advice {
    position: relative;
    display: flex;
    flex-flow: column;
    align-items: center;
    gap: 1rem;
    box-shadow: 0 0 4px #ccc;
    padding: 1rem;
    height: 20rem;
    margin: 4rem 6rem;
    border-radius: 1rem;
    color: white;
  }
  .dice {
    position: absolute;
    z-index: 800;
    margin: auto;
    top: 47%;
    display: flex;
    justify-content: space-around;
    align-items: center;
    background-color: cyan;
  }
  @media screen and (max-width:480px) {
    main {
      margin: inherit 1vw;
    }
    .dice {
      top: 52%;
    }
  }
</style>

<main>
  <div class="flex flex-col items-center justify-around md:h-[30vh] h-[80%] rounded-lg m-auto bg-gray-400 md:my-[4rem] mt-[2rem] md:mx-[4rem] mx-[2rem]">
    <div class="text-lg font-mono text-teal-200">Advice #{data.id}</div>
    <div class="text-xl text-center">"{data.text}"</div>
    <div class="hidden mb-[1rem]"><img src="/images/pattern-divider-desktop.svg" alt="divider"></div>
    <div class="visible"><img src="/images/pattern-divider-mobile.svg" alt="divider"></div>
    <button on:click={getData} class="dice flex items-center justify-around bg-cyan-100 w-[3rem] h-[3rem] rounded-full">
      <img src="/images/icon-dice.svg" alt="dice">
    </button>
  </div>
</main>