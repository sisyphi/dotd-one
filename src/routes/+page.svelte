<script lang="ts">
	import RedLightGreenLight from '$lib/components/RedLightGreenLight.svelte';
	import { Confetti } from 'svelte-confetti';

	let isGameWonD = $state(false);
	let isGameWonF = $state(false);
	let isGameWonJ = $state(false);
	let isGameWonK = $state(false);
</script>

<div
	class="flex h-full scale-50 flex-row items-center justify-center gap-8 py-8 md:scale-100 md:gap-12"
>
	<RedLightGreenLight key="d" bind:isGameWon={isGameWonD} />
	<RedLightGreenLight key="f" bind:isGameWon={isGameWonF} />
	<RedLightGreenLight key="j" bind:isGameWon={isGameWonJ} />
	<RedLightGreenLight key="k" bind:isGameWon={isGameWonK} />
</div>
{#if isGameWonD && isGameWonF && isGameWonJ && isGameWonK}
	<div
		class="pointer-events-none fixed -top-12 left-0 flex h-svh w-svw flex-row justify-center overflow-hidden"
	>
		<Confetti
			x={[-5, 5]}
			y={[0, 0.1]}
			size={30}
			colorArray={['#ffffff']}
			infinite
			duration={5000}
			amount={200}
			fallDistance="100svh"
		/>
	</div>
{/if}
