<script lang="ts">
	import RedLightGreenLight from '$lib/components/RedLightGreenLight.svelte';
	import { Confetti } from 'svelte-confetti';

	let isGameWonD = $state(false);
	let isGameWonF = $state(false);
	let isGameWonJ = $state(false);
	let isGameWonK = $state(false);
</script>

<div class="flex flex-row items-center justify-center h-full gap-12">
	<RedLightGreenLight key="d" bind:isGameWon={isGameWonD} />
	<RedLightGreenLight key="f" bind:isGameWon={isGameWonF} />
	<RedLightGreenLight key="j" bind:isGameWon={isGameWonJ} />
	<RedLightGreenLight key="k" bind:isGameWon={isGameWonK} />
	{#if isGameWonD && isGameWonF && isGameWonJ && isGameWonK}
		<div
			class="-top-12 h-svh w-svw fixed left-0 flex flex-row justify-center overflow-hidden pointer-events-none"
		>
			<Confetti
				x={[-5, 5]}
				y={[0, 0.1]}
				size={30}
				colorArray={['#ffffff']}
				infinite
				duration={5000}
				amount={200}
				fallDistance="100vh"
			/>
		</div>
	{/if}
</div>
