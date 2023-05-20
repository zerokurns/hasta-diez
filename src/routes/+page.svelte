<script lang="ts">
	import { writable } from 'svelte/store'
	import { AppShell } from '@skeletonlabs/skeleton'
	import { Timer } from 'timer-node'
	const timer = new Timer()

	const readyToBegin = 'yes king'

	let rep = 0
	let restCounter = writable('')

	const countRep = () => {
		timer.clear()
		rep += 1
		if (rep <= 9) {
			startTimer()
		} else {
			reset()
		}
	}

	const startTimer = () => {
		timer.clear()
		timer.start()
		setInterval(() => {
			restCounter.set(timer.format('%mm %ss'))
		}, 100)
	}

	const reset = () => {
		rep = 0
		timer.clear()
	}
</script>

<AppShell>
	<svelte:fragment slot="header">
		<div class="flex justify-center my-10">
			Hasta Diez
			{#if rep > 0}
				<button id="reset-button" class="btn text-error-200-700-token m-4" on:click={reset}
					><svg
						xmlns="http://www.w3.org/2000/svg"
						class="icon icon-tabler icon-tabler-rotate-clockwise"
						width="24"
						height="24"
						viewBox="0 0 24 24"
						stroke-width="1"
						stroke="currentColor"
						fill="none"
						stroke-linecap="round"
						stroke-linejoin="round"
					>
						<path stroke="none" d="M0 0h24v24H0z" fill="none" />
						<path d="M4.05 11a8 8 0 1 1 .5 4m-.5 5v-5h5" />
					</svg></button
				>
			{/if}
		</div>
	</svelte:fragment>

	<div class="h-full text-center flex flex-col items-center justify-evenly p-10">
		<button class="btn btn-xl text-9xl h-full w-full" on:click={countRep}>
			{rep}
		</button>
	</div>

	<svelte:fragment slot="footer">
		<div class="flex justify-center my-10 text-4xl">
			{#if rep > 0 }
				{$restCounter}
			{:else}
				{readyToBegin}
			{/if}
		</div>
	</svelte:fragment>
</AppShell>

<style>
	#reset-button {
		position: absolute;
		top: 0;
		left: 0;
	}
</style>
