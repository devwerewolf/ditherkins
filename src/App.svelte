<script>
	// Lib
	import { onMount } from "svelte";
  import Wave from "@foobar404/wave";

	// Components
	import HexButton from "./components/HexButton.svelte";
	
	// Variables
	let hexButtons = [
		{ label: "#", soundBite: "hit1" },
		{ label: "e", soundBite: "celebrate2" },
		{ label: "1", soundBite: "celebrate1" },
		{ label: "0", soundBite: "idle1" },
		{ label: "0", soundBite: "idle2" },
		{ label: "9", soundBite: "celebrate3" },
		{ label: "8", soundBite: "celebrate4" },
	];
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
	<div class="title-card">
		<h1>The Official Dither Soundboard™</h1>
		<h2>Made with 💜 by WerewolfDev</h2>
	</div>
</header>

<main>
	{#each hexButtons as hexButton}
		<HexButton {...hexButton} on:playSoundBite={onPlaySoundBite}/>
	{/each}
</main>

<canvas id="sound-visualizer" {height} {width}></canvas>

<style>
	header {
		color: white;
		position: absolute;
	}
	
	header img {
		position: fixed;
		top: 0;
		right: 0;
	}
	
	header .title-card {
		font-size: 2vh;
		transform: translateY(12vh);
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