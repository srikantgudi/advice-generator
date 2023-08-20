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
    margin: auto;
    bottom: -5%;
    background-color: white;
    border-radius: 0.5rem;
  }
  .divider-desktop {
    display: block;
    position: absolute;
    bottom: 11%;
  }
  .divider-mobile {
    display: none;
    position: absolute;
    bottom: 11%;
  }
  @media screen and (max-width:480px) {
    main {
      margin: inherit 1vw;
    }
    .divider-desktop {
      display: none;
    }
    .divider-mobile {
      display: block;
    }
  }
</style>

<main>
  <div class="advice my-[4rem]">
    <div class="text-xl font-mono">Advice #{data.id}</div>
    <div class="text-2xl text-center">"{data.text}"</div>
    <div class="mt-5 divider-desktop"><img src="/images/pattern-divider-desktop.svg" alt="divider"></div>
    <div class="mt-5 divider-mobile"><img src="/images/pattern-divider-mobile.svg" alt="divider"></div>
    <button on:click={getData} class="dice bg-white-100 text-2xl text-white-200"><img src="/images/icon-dice.svg" width="40" alt="dice"></button>
  </div>
</main>