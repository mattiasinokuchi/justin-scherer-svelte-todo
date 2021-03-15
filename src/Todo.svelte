<!-- This file contain logic for the individual todo -->

<script>
	import { createEventDispatcher } from 'svelte';
	export let completed;
	export let num;
	export let description;

	const dispatch = createEventDispatcher();
</script>

<style>
	.completed {
		text-decoration: line-through;
	}
</style>

<li class:completed>
	Task {num}: {description}
	<input type="checkbox" bind:checked={completed} />
	<button on:click="{() => dispatch('remove', null)}">Remove</button>
</li>