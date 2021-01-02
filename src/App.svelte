<script>
</script>

<div class="kalimba">
	<div class="tines">
		<div class="tine">D</div>
		<div class="tine">C</div>
		<div class="tine">E</div>
	</div>
</div>

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
	
	.tine {
		background: peachpuff;
		height: 100px;
		display: flex;
		align-items: end;
		padding: 10px;
		color: tomato;
		font-weight: bold;
		border-radius: 0 0 10px 10px;
	}
</style>