<script lang="ts">
	import { Timer } from 'timer-node'
	const timer = new Timer()

	let rep = 0
	let isResting = false
	let restCounter = ''

	const countRep = () => {
		if (rep < 9) {
			rep += 1
		} else {
			isResting = true
			timer.clear()
			startTimer()
		}
	}

	const startTimer = () => {
		timer.start()
		console.log(timer.time())
		setInterval(() => {
			restCounter = timer.format('%mm %ss')
		}, 100)
	}

	const resetRest = () => {
		rep = 0
		isResting = false
		timer.clear()
	}

	const resetCounter = () => {
		rep = 0
	}
</script>

<div class="container h-full mx-auto flex justify-center items-center">
	<div class="space-y-10 text-center flex flex-col items-center">
		<h2 class="h2 font-bold">Hasta Diez</h2>
		<div class="container mx-auto flex px-5 items-center justify-center flex-col">
			<h1 class="title-font text-9xl m-10 font-medium">
				{#if isResting}
					{restCounter}
				{:else}
					{rep}
				{/if}
			</h1>
			<div class="flex justify-center">
				{#if isResting}
					<button class="btn variant-primary-filled" on:click={resetRest}
						><svg
							xmlns="http://www.w3.org/2000/svg"
							class="icon icon-tabler icon-tabler-hourglass-off"
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
							<path d="M18 18v2a1 1 0 0 1 -1 1h-10a1 1 0 0 1 -1 -1v-2a6 6 0 0 1 6 -6" />
							<path d="M6 6a6 6 0 0 0 6 6m3.13 -.88a6 6 0 0 0 2.87 -5.12v-2a1 1 0 0 0 -1 -1h-10" />
							<path d="M3 3l18 18" />
						</svg></button
					>
				{:else}
					<button class="btn variant-primary-filled" on:click={countRep}
						><svg
							xmlns="http://www.w3.org/2000/svg"
							class="icon icon-tabler icon-tabler-plus"
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
							<path d="M12 5l0 14" />
							<path d="M5 12l14 0" />
						</svg></button
					>
				{/if}
			</div>
		</div>
	</div>
</div>

{#if ~isResting}
	<button id="reset-button" class="btn variant-ringed-primary" on:click={resetCounter}
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

<style>
	#reset-button {
		position: absolute;
		top: 0;
		left: 0;
	}
</style>
