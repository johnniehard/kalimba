<script>
	let c4;
	let active = false;
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

	.tine {
		user-select: none;
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

<div class="kalimba">
	<div class="tines">
		<div class="tine">D</div>
		<div
			class="tine"
			on:mousedown={() => {
				active = true;
			}}
			on:touchstart={() => {
				active = true;
				c4.currentTime = 0;
					c4.play();
			}}
			on:mouseup={() => {
				active = false;
			}}
			on:touchend={() => {
				active = false;
			}}
			on:mouseleave={() => {
				if (active) {
					c4.currentTime = 0;
					c4.play();
				}
			}}
			on:touchleave={() => {
				if (active) {
					c4.currentTime = 0;
					c4.play();
				}
			}}>
			C
			<audio bind:this={c4} src="/C4.wav" />
		</div>
		<div class="tine">E</div>
	</div>
</div>
