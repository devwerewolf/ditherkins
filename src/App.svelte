<script>
	// Lib
	import { onMount } from "svelte";
  import Wave from "@foobar404/wave";

	// Components
	import HexButton from "./components/HexButton.svelte";
	
	// Variables
	let labels = ["#", "e", "1", "0", "0", "9", "8"];
	let height;
	let width;
	let wave;
	
	// Functions
	function onPlaySoundBite(e) {
		const {soundBite, audioEl} = e.detail;
		
		wave = new Wave();
    wave.fromElement(`sound-bite-${soundBite}`, "sound-visualizer", {
      type: "cubes",
      colors: ["#00aaff", "#f7e27b", "#e10098"]
		});
		
		audioEl.play();
	}
</script>


<svelte:window bind:innerHeight={height} bind:innerWidth={width}/>

<header>
	<img src="images/plant.png" height="128px" width="128px" alt="Dithered">
</header>

<main>
	<HexButton label="#" soundBite="hit1" on:playSoundBite={onPlaySoundBite}/>
	<HexButton label="e" soundBite="celebrate2" on:playSoundBite={onPlaySoundBite}/>
	<HexButton label="1" soundBite="celebrate1"/>
	<HexButton label="0" soundBite="idle1"/>
	<HexButton label="0" soundBite="idle2"/>
	<HexButton label="9" soundBite="celebrate3"/>
	<HexButton label="8" soundBite="celebrate4"/>
</main>

<canvas id="sound-visualizer" {height} {width}></canvas>

<style>
	header {
		position: fixed;
		top: 0;
		right: 0;
	}
	
	main {
		text-align: center;
    user-select: none;
	}
	
	canvas {
		bottom: 0;
		height: 100%;
		position: fixed;
		width: 100%;
		z-index: -1;
	}
</style>