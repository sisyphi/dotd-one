<script lang="ts">
	// import { gsap } from 'gsap/dist/gsap';
	type PropsType = {
		key: string;
		maxVal?: number;
		minInterval?: number;
		intervalRange?: number;
		timer?: number;
		test?: number;
		isGameWon: boolean;
	};

	let {
		key = 'j',
		maxVal = 5,
		minInterval = 1,
		intervalRange = 3,
		timer = 2,
		isGameWon = $bindable(false)
	}: PropsType = $props();

	let isBtnDown: boolean = $state(false);
	let val: number = $state(0);

	let isEyeOpen: boolean = $state(true);

	let isGameLost: boolean = $state(false);

	let eyeCooldown: number = $state(timer);

	function handleKeydown(event: { key: any }) {
		if (event.key === key) {
			isBtnDown = true;
		}
	}

	function handleKeyup(event: { key: any }) {
		if (event.key === key) {
			isBtnDown = false;
		}
	}

	setInterval(() => {
		if (!isGameLost && !isGameWon) {
			if (isBtnDown) val += 0.1;
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
		if (isBtnDown) {
			if (isEyeOpen && !(isEyeOpen && eyeCooldown > timer - coyoteTime)) {
				isGameLost = true;
			}
		}
		if (val >= maxVal) {
			isGameWon = true;
			console.log('won');
		}
	});

	let eyeLidStyle = $state('top-1/2 size-24');

	$effect(() => {
		if (isGameLost || isGameWon) {
			eyeLidStyle = '-top-full size-24';
		} else if (isEyeOpen) {
			eyeLidStyle = '-top-1 size-32';
		} else {
			eyeLidStyle = 'top-1/2 size-24';
		}
	});
</script>

<svelte:window onkeydown={handleKeydown} onkeyup={handleKeyup} />

<div
	id="container"
	class="flex h-full flex-col gap-8 border-8 border-white bg-black p-6
	{isGameLost || isGameWon
		? ''
		: Math.round((val / maxVal) * 100) > 75
			? 'strong-hover-shake'
			: Math.round((val / maxVal) * 100) > 50
				? 'weak-hover-shake'
				: ''}"
>
	<div
		id="eye"
		class="relative mx-auto size-24 flex-none overflow-hidden rounded-full border-8 border-white p-4
		{isGameWon ? 'bg-black' : 'bg-white'}"
	>
		<div id="eye-lid" class="eye-lid {eyeLidStyle}"></div>
		<div
			id="eye-ball"
			class="eye-ball
			{isGameWon ? 'top-1/2 size-16 bg-white' : 'top-[60%] size-12 bg-black'}"
		></div>
	</div>
	<div
		id="progress-container"
		class="mx-auto flex w-fit flex-grow flex-col-reverse border-8 border-white p-2"
	>
		<div
			id="progress-val"
			class="w-4 bg-white transition-all"
			style="height: {Math.min(Math.round((val / maxVal) * 100), 100)}%;"
		></div>
	</div>
	<div
		id="btn"
		class="disable-selection mx-auto flex size-16 flex-none flex-col justify-center border-8 border-white
		{isBtnDown ? 'translate-y-0 bg-white' : '-translate-y-2 bg-black'}"
	>
		<button
			class="font-sans text-3xl font-thin
			{isBtnDown ? 'text-black' : 'text-white'}"
			ontouchstart={() => {
				isBtnDown = true;
			}}
			ontouchend={() => {
				isBtnDown = false;
			}}
			onmousedown={() => {
				isBtnDown = true;
			}}
			onmouseup={() => {
				isBtnDown = false;
			}}
		>
			{key.toUpperCase()}
		</button>
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
		border-radius: 100%;
		left: 50%;
		position: absolute;
		transform: translate(-50%, -50%);
		z-index: 1;
		transition: 0.35s all;
	}

	.disable-selection {
		-webkit-touch-callout: none;
		-webkit-user-select: none;
		-khtml-user-select: none;
		-moz-user-select: none;
		-ms-user-select: none;
		user-select: none;
		outline: 0;
	}

	.weak-hover-shake {
		animation: tilt-shaking 0.5s infinite;
	}

	.strong-hover-shake {
		animation: tilt-shaking 0.25s infinite;
	}

	@keyframes tilt-shaking {
		0% {
			transform: rotate(0deg);
		}
		25% {
			transform: rotate(0.5deg);
		}
		50% {
			transform: rotate(0eg);
		}
		75% {
			transform: rotate(-0.5deg);
		}
		100% {
			transform: rotate(0deg);
		}
	}
</style>
