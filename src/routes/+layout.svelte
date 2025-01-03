<script lang="ts">
	import '../app.css';
	let { children } = $props();

	let bgPosition: number = $state(0);
	const xDir = Math.random() > 0.5 ? 1 : -1;
	const yDir = Math.random() > 0.5 ? 1 : -1;

	setInterval(() => {
		bgPosition = Math.round(((bgPosition + 0.1) % 100) * 100) / 100;
	}, 0.1);

	const bgs = ['bg-triangle', 'bg-moon', 'bg-polka'];
</script>

<div class="h-svh flex flex-col">
	<header class="flex flex-row justify-center h-24 bg-black border-b-8 border-white">
		<h1 class="self-center font-sans text-5xl font-thin text-white">
			{'ONE'}<span class="text-2xl">{' by sisyphi'}</span>
		</h1>
	</header>
	<div
		class="{bgs[Math.round(Math.random() * 2)]} h-full flex-1 bg-black"
		style="background-position: {`${bgPosition * xDir}px ${bgPosition * yDir}px`};"
	>
		{@render children()}
	</div>
	<footer class="flex flex-col justify-center w-full h-24 bg-black border-t-8 border-white">
		<p class="self-center justify-center font-sans text-2xl font-thin text-white">
			finish all four to win.
		</p>
		<p class="self-center justify-center font-sans text-2xl font-thin text-white">
			reload page to play again.
		</p>
	</footer>
</div>

<style>
	.bg-polka {
		background-color: #000000;
		opacity: 1;
		background-image: radial-gradient(#818181 2px, transparent 2px),
			radial-gradient(#818181 2px, #000000 2px);
		background-size: 100px 100px;
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
		background-size: 100px 100px;
	}

	.bg-triangle {
		background-color: #000000;
		opacity: 1;
		background-image: linear-gradient(-45deg, #000000, #000000 50%, #252525 50%, #252525);
		background-size: 100px 100px;
	}
</style>
