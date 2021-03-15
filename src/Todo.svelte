<!-- This file contain logic for the individual todo -->

<svelte:options accessors={true} />
<script>
	import { createEventDispatcher } from 'svelte';
	export let completed = false;
	export let num = null;
	export let description = null;
	export let dueDate = null;
	export let hidden = false;

	const dispatch = createEventDispatcher();
</script>

<style>
	.completed {
		text-decoration: line-through;
	}
	.hidden {
		display: none;
	}
</style>

<li class:completed class:hidden>
	Task {num}: {description} - Due on {dueDate}
	<input type="checkbox" bind:checked={completed} />
	<button on:click="{() => dispatch('remove', null)}">Remove</button>
</li>