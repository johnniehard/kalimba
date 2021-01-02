<script>
	import Tine from './Tine.svelte'

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

<div class="kalimba">
	<div class="tines">
		<Tine note="D" />
		<Tine note="C" />
		<Tine note="E" />
	</div>
</div>
