<script>
  // Lib
  import { createEventDispatcher } from "svelte";
  
  // Props
  export let label = "";
  export let soundBite = "";
  
  // Elements
  let audioEl;
  
  // Constants
  const dispatch = createEventDispatcher();
  
  // Functions
  function playSoundBite() {
    dispatch("playSoundBite", { audioEl, soundBite });
  }
</script>


<svelte:options accessors />

<main>
  <h1 on:click={playSoundBite}>{label}</h1>
</main>

<!-- svelte-ignore a11y-media-has-caption -->
<audio id="sound-bite-{soundBite}" bind:this={audioEl}>
	<source src="sounds/{soundBite}.ogg" type="audio/ogg">
</audio>


<style>
  main {
    display: inline-block;
    cursor: pointer;
    transform: translateY(32vh);
    user-select: none;
  }
  
  h1 {
		color: #e10098;
		font-size: 11vh;
  }
</style>