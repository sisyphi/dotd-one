<script lang="ts">
	import '../app.css';
	let { children } = $props();

	let bgOffset: number = $state(0);

	setInterval(() => {
		bgOffset = (bgOffset + 0.1) % 120;
	}, 0.1);
</script>

<div class="flex h-svh flex-col">
	<header class="flex h-24 w-full flex-row justify-center border-b-8 border-white bg-black">
		<h1 class="self-center font-sans text-5xl font-thin text-white">one by sisyphi</h1>
	</header>
	<div
		class="bg-moon h-full flex-1 bg-black"
		style="background-position: {`${-Math.round(bgOffset * 100) / 100}px ${-Math.round(bgOffset * 100) / 100}px`};"
	>
		{@render children()}
	</div>
	<footer class="h-24 w-full border-t-8 border-white bg-black">FOOTER</footer>
</div>

<style>
	.bg-diagonal {
		background-color: #000000;
		opacity: 1;
		background: repeating-linear-gradient(-45deg, #363636, #363636 3px, #000000 3px, #000000 17px);
		background-size: 25%;
	}

	.bg-vert-lines {
		background-color: #000000;
		opacity: 1;
		background-size: 46px 46px;
		background-image: repeating-linear-gradient(
			to right,
			#363636,
			#363636 2.3000000000000003px,
			#000000 2.3000000000000003px,
			#000000
		);
	}

	.bg-isometric {
		background-color: #000000;
		opacity: 1;
		background-image: linear-gradient(
				30deg,
				#363636 12%,
				transparent 12.5%,
				transparent 87%,
				#363636 87.5%,
				#363636
			),
			linear-gradient(
				150deg,
				#363636 12%,
				transparent 12.5%,
				transparent 87%,
				#363636 87.5%,
				#363636
			),
			linear-gradient(
				30deg,
				#363636 12%,
				transparent 12.5%,
				transparent 87%,
				#363636 87.5%,
				#363636
			),
			linear-gradient(
				150deg,
				#363636 12%,
				transparent 12.5%,
				transparent 87%,
				#363636 87.5%,
				#363636
			),
			linear-gradient(
				60deg,
				#36363677 25%,
				transparent 25.5%,
				transparent 75%,
				#36363677 75%,
				#36363677
			),
			linear-gradient(
				60deg,
				#36363677 25%,
				transparent 25.5%,
				transparent 75%,
				#36363677 75%,
				#36363677
			);
		background-size: 80px 140px;
		background-position:
			0 0,
			0 0,
			40px 70px,
			40px 70px,
			0 0,
			40px 70px;
	}

	.bg-moon {
		background-color: #000000;
		opacity: 1;
		background-image: radial-gradient(
			ellipse farthest-corner at 90px 90px,
			#363636,
			#363636 50%,
			#000000 50%
		);
		background-size: 120px 120px;
	}
</style>
