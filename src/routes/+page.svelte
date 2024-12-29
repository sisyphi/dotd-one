<script lang="ts">
	let isKeyDown: boolean = $state(false);
	let val: number = $state(0);
	const maxVal: number = 5;

	setInterval(() => {
		if (!isGameLost && !isGameWon) {
			if (isKeyDown) val += 0.1;
		}
	}, 100);

	function handleKeydown(event: { key: any }) {
		if (event.key === 'j') isKeyDown = true;
	}

	function handleKeyup(event: { key: any }) {
		if (event.key === 'j') isKeyDown = false;
	}

	let isEyeOpen: boolean = $state(false);
	let eyeCooldown: number = $state(0);
	const minInterval: number = 1;
	const intervalRange: number = 4;

	setInterval(() => {
		if (!isGameLost && !isGameWon) {
			eyeCooldown -= 0.1;
			if (eyeCooldown <= 0) {
				isEyeOpen = !isEyeOpen;
				eyeCooldown = Math.random() * intervalRange + minInterval;
			}
		}
	}, 100);

	let isGameLost: boolean = $state(false);
	let isGameWon: boolean = $state(false);

	$effect(() => {
		if (isEyeOpen && isKeyDown) isGameLost = true;
		if (val >= maxVal) isGameWon = true;
	});
</script>

<svelte:window onkeydown={handleKeydown} onkeyup={handleKeyup} />

<div id="container" class="bg-blue-50 flex flex-col gap-4 py-8">
	<div
		id="eye"
		class="mx-auto mb-4 size-24 rounded-full border-8 border-black p-4 {isEyeOpen
			? ''
			: 'bg-black'}"
	>
		<div id="progress-val" class="size-full mx-auto bg-black rounded-full"></div>
	</div>
	<div
		id="progress-container"
		class="w-fit rounded-2xl flex flex-col-reverse h-64 p-1 mx-auto border-8 border-black"
	>
		<div
			id="progress-val"
			class="w-5 bg-black rounded-md"
			style="height: {Math.min(Math.round((val / maxVal) * 100), 100)}%;"
		></div>
	</div>
	<div
		id="btn"
		class="size-16 rounded-2xl flex flex-col justify-center mx-auto border-8 border-black"
	>
		<button class="font-mono text-3xl font-black">{isKeyDown}</button>
	</div>

	<div>{val}</div>
	<div>{Math.min(Math.round((val / maxVal) * 100), 100)}</div>
	<div>{isEyeOpen}, {Math.round(eyeCooldown * 10) / 10}</div>
	<div>{isGameLost}, {isGameWon}</div>
</div>
