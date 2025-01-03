<script lang="ts">
	// import { gsap } from 'gsap/dist/gsap';
	let { key, maxVal = 5, minInterval = 1, intervalRange = 3, timer = 2 } = $props();

	let isKeyDown: boolean = $state(false);
	let val: number = $state(0);

	let isEyeOpen: boolean = $state(true);

	let isGameLost: boolean = $state(false);
	let isGameWon: boolean = $state(false);

	let eyeCooldown: number = $state(timer);

	function handleKeydown(event: { key: any }) {
		if (event.key === key) {
			isKeyDown = true;
		}
	}

	function handleKeyup(event: { key: any }) {
		if (event.key === key) {
			isKeyDown = false;
		}
	}

	setInterval(() => {
		if (!isGameLost && !isGameWon) {
			if (isKeyDown) val += 0.1;
		}
	}, 100);

	// Eye handler
	let coyoteTime: number = 0.35;
	setInterval(() => {
		if (!isGameLost && !isGameWon) {
			eyeCooldown = Math.round((eyeCooldown - 0.1) * 100) / 100;
			if (eyeCooldown <= 0) {
				isEyeOpen = !isEyeOpen;

				timer = Math.round((Math.random() * intervalRange + minInterval) * 100) / 100;
				eyeCooldown = timer;
			}
		}
	}, 100);

	// Game handler
	$effect(() => {
		if (isKeyDown) {
			if (isEyeOpen && !(isEyeOpen && eyeCooldown > timer - coyoteTime)) {
				isGameLost = true;
			}
		}
		if (val >= maxVal) isGameWon = true;
	});

	let eyeLidStyle = $state('top-1/2 size-24');

	$effect(() => {
		if (isGameLost) {
			eyeLidStyle = '-top-full size-24';
		} else if (isGameWon) {
			eyeLidStyle = 'top-1/2 size-24';
		} else if (isEyeOpen) {
			eyeLidStyle = '-top-1 size-32';
		} else {
			eyeLidStyle = 'top-1/2 size-24';
		}
	});
</script>

<svelte:window onkeydown={handleKeydown} onkeyup={handleKeyup} />

<div id="container" class="flex h-fit flex-col gap-8 border-8 border-white bg-black p-8">
	<div
		id="eye"
		class="relative mx-auto size-24 overflow-hidden rounded-full border-8 border-white bg-white p-4"
	>
		<div id="eye-lid" class="eye-lid {eyeLidStyle}"></div>
		<div id="eye-ball" class="eye-ball"></div>
	</div>
	<div
		id="progress-container"
		class="mx-auto flex h-64 w-fit flex-col-reverse border-8 border-white p-2"
	>
		<div
			id="progress-val"
			class="w-4 bg-white transition-all"
			style="height: {Math.min(Math.round((val / maxVal) * 100), 100)}%;"
		></div>
	</div>
	<div
		id="btn"
		class="mx-auto flex size-16 flex-col justify-center border-8 border-white {isGameWon
			? 'bg-white'
			: ''}  {isKeyDown && !isGameWon ? 'translate-y-2 bg-white' : ''}"
	>
		<button class="font-mono text-3xl {isKeyDown && !isGameWon ? 'text-black' : 'text-white'}"
			>{key}</button
		>
	</div>
</div>

<style>
	.eye-lid {
		background-color: black;
		height: 6.5rem;
		border-radius: 100%;
		left: 50%;
		position: absolute;
		transform: translate(-50%, -50%);
		z-index: 999;
		transition: 0.35s all;
	}

	.eye-ball {
		background-color: black;
		width: 3rem;
		height: 3rem;
		border-radius: 100%;
		top: 60%;
		left: 50%;
		position: absolute;
		transform: translate(-50%, -50%);
		z-index: 1;
	}
</style>
