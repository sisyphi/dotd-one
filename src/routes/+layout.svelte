<script lang="ts">
	import '../app.css';
	let { children } = $props();

	let bgPosition: number = $state(0);
	const xDir = Math.random() > 0.5 ? 1 : -1;
	const yDir = Math.random() > 0.5 ? 1 : -1;
	const bgs = ['bg-triangle', 'bg-moon', 'bg-polka'];
	const randChoice = Math.round(Math.random() * 2);
	const bgPattern = bgs[randChoice];

	setInterval(() => {
		bgPosition = Math.round(((bgPosition + 0.1) % 100) * 100) / 100;
	}, 0.1);
</script>

<div class="flex h-svh flex-col">
	<header class="flex h-24 flex-none flex-row justify-center border-b-8 border-white bg-black">
		<h1 class="self-center font-sans text-5xl font-thin text-white">
			{'ONE'}<span class="text-2xl">{' by sisyphi'}</span>
		</h1>
	</header>
	<div
		class="h-24 flex-1 flex-grow bg-black {bgPattern}"
		style="background-position: {`${bgPosition * xDir}px ${bgPosition * yDir}px`};"
	>
		{@render children()}
	</div>
	<footer
		class="flex h-36 w-full flex-none flex-col justify-center border-t-8 border-white bg-black"
	>
		<p class="justify-center self-center font-sans text-2xl font-thin text-white">
			press the buttons to fill the bars.
		</p>
		<p class="justify-center self-center font-sans text-2xl font-thin text-white">
			only press when the eyes are closed.
		</p>
		<p class="justify-center self-center font-sans text-2xl font-thin text-white">
			reload the page to play again.
		</p>
	</footer>
</div>

<style>
	.bg-polka {
		background-color: #000000;
		opacity: 1;
		background-image: radial-gradient(#818181 2px, transparent 2px),
			radial-gradient(#818181 2px, #000000 2px);
		background-size: 50px 50px;
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
