<script>
	import * as Tone from "tone";
	import { scaleLinear } from "d3-scale";
	import { extent } from 'd3-array'
	import Tine from "./Tine.svelte";

	let started = false;
	let loading = true;

	let height;

	const notes = [
		{ name: "D6", freq: 1174 },
		{ name: "B5", freq: 987.7 },
		{ name: "G5", freq: 783.9 },
		{ name: "E5", freq: 659.2 },
		{ name: "C5", freq: 523.2 },
		{ name: "A4", freq: 440 },
		{ name: "F4", freq: 349.2 },
		{ name: "D4", freq: 293.6 },
		{ name: "C4", freq: 261.6 },
		{ name: "E4", freq: 329.6 },
		{ name: "G4", freq: 391.9 },
		{ name: "B4", freq: 493.8 },
		{ name: "D5", freq: 587.3 },
		{ name: "F5", freq: 698.4 },
		{ name: "A5", freq: 880 },
		{ name: "C6", freq: 1046 },
		{ name: "E6", freq: 1318 },
	];

	const notesExtent = extent(notes, d => d.freq)
	let tineSizeScale = scaleLinear(notesExtent, [500, 50])

	const sampler = new Tone.Sampler({
		urls: {
			C4: "C4.wav",
		},
		baseUrl: "/",
	}).toDestination();

	Tone.loaded().then(() => {
		loading = false;
	});

	$: if(started) {
		tineSizeScale = tineSizeScale.range([height, 50])
	}
</script>

<style>
	.kalimba {
		display: flex;
		justify-content: center;
		background: salmon;
		height: 100%;
		padding: 20px;
	}

	.tines {
		background: orange;
		height: 100%;
		align-self: start;
		justify-content: center;
		padding: 30px;
		padding-top: 0;
		display: flex;
		align-items: start;
		border-radius: 30px;
		gap: 10px;
	}
</style>

{#if loading}
	<p>loading</p>
{:else if !started}
	<button
		on:click|preventDefault={async () => {
			await Tone.start();
			document.documentElement.requestFullscreen();
			started = true;
		}}>
		Start Tone
	</button>
{:else}
	<div class="kalimba">
		<div class="tines" bind:clientHeight={height}>
			{#each notes as note}
				<Tine {note} {sampler} size={tineSizeScale(note.freq)}/>
			{/each}
		</div>
	</div>
{/if}
