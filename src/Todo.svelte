<!-- This file contain logic for the individual todo -->

<script>
	import { createEventDispatcher } from 'svelte';
	export let completed;
	export let num;
	export let description;
	export let dueDate;

	const dispatch = createEventDispatcher();
</script>

<style>
	.completed {
		text-decoration: line-through;
	}
</style>

<li class:completed>
	Task {num}: {description} Due on {dueDate}
	<input type="checkbox" bind:checked={completed} />
	<button on:click="{() => dispatch('remove', null)}">Remove</button>
</li>