<script lang="ts">
	import '../app.css';
	let { children } = $props();

	let bgOffset: number = $state(0);

	setInterval(() => {
		bgOffset = (bgOffset + 0.1) % 100;
	}, 0.1);
</script>

<div class="flex h-svh flex-col">
	<header class="flex h-24 w-full flex-row justify-center border-b-8 border-white bg-black">
		<h1 class="self-center font-sans text-5xl font-thin text-white">
			{'ONE'}<span class="text-2xl">{' by sisyphi'}</span>
		</h1>
	</header>
	<div
		class="bg-triangle h-full flex-1 bg-black"
		style="background-position: {`${Math.round(bgOffset * 100) / 100}px ${Math.round(bgOffset * 100) / 100}px`};"
	>
		{@render children()}
	</div>
	<footer class="h-24 w-full border-t-8 border-white bg-black"></footer>
</div>

<style>
	.bg-polka {
		background-color: #000000;
		opacity: 1;
		background-image: radial-gradient(#818181 2px, transparent 2px),
			radial-gradient(#818181 2px, #000000 2px);
		background-size: 100px 100px;
	}
	.bg-diagonal {
		background-color: #000000;
		opacity: 1;
		background: repeating-linear-gradient(-45deg, #363636, #363636 3px, #000000 3px, #000000 17px);
		background-size: 24px;
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
				#252525 12%,
				transparent 12.5%,
				transparent 87%,
				#252525 87.5%,
				#252525
			),
			linear-gradient(
				150deg,
				#252525 12%,
				transparent 12.5%,
				transparent 87%,
				#252525 87.5%,
				#252525
			),
			linear-gradient(
				30deg,
				#252525 12%,
				transparent 12.5%,
				transparent 87%,
				#252525 87.5%,
				#252525
			),
			linear-gradient(
				150deg,
				#252525 12%,
				transparent 12.5%,
				transparent 87%,
				#252525 87.5%,
				#252525
			),
			linear-gradient(
				60deg,
				#25252577 25%,
				transparent 25.5%,
				transparent 75%,
				#25252577 75%,
				#25252577
			),
			linear-gradient(
				60deg,
				#25252577 25%,
				transparent 25.5%,
				transparent 75%,
				#25252577 75%,
				#25252577
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

	.bg-triangle {
		background-color: #000000;
		opacity: 1;
		background-image: linear-gradient(-45deg, #000000, #000000 50%, #252525 50%, #252525);
		background-size: 100px 100px;
	}

	.bg-cross {
		background-color: #e5e5f7;
		opacity: 0.8;
		background:
			radial-gradient(
				circle,
				transparent 20%,
				#e5e5f7 20%,
				#e5e5f7 80%,
				transparent 80%,
				transparent
			),
			radial-gradient(
					circle,
					transparent 20%,
					#e5e5f7 20%,
					#e5e5f7 80%,
					transparent 80%,
					transparent
				)
				25px 25px,
			linear-gradient(#444cf7 2px, transparent 2px) 0 -1px,
			linear-gradient(90deg, #444cf7 2px, #e5e5f7 2px) -1px 0;
		background-size:
			50px 50px,
			50px 50px,
			25px 25px,
			25px 25px;
	}
</style>
