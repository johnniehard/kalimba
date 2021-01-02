<script>
	import * as Tone from "tone";

	import Tine from "./Tine.svelte";

	let started = false;
	let loading = true;

	const sampler = new Tone.Sampler({
		urls: {
			"C4": "C4.wav",
		},
		baseUrl: "/",
	}).toDestination()

	Tone.loaded().then(() => {
		loading = false
	})

</script>

<style>
	.kalimba {
		display: flex;
		justify-content: center;
		background: salmon;
		height: 100%;
	}

	.tines {
		background: orange;
		align-self: start;
		justify-content: center;
		padding: 20px;
		padding-top: 0;
		display: flex;
		align-items: start;
		border-radius: 0 0 30px 30px;
		gap: 10px;
	}
</style>

{#if loading}
	<p>loading</p>
{:else if !started}
	<button
		on:click|preventDefault={async () => {
			await Tone.start();
			started = true;
		}}>
		Start Tone
	</button>
{:else}
	<div class="kalimba">
		<div class="tines">
			<Tine note="D4" {sampler}/>
			<Tine note="C4" {sampler}/>
			<Tine note="E4" {sampler}/>
		</div>
	</div>
{/if}
