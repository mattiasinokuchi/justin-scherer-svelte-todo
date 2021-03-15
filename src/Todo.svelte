<!-- This file contain logic for the individual todo -->

<svelte:options accessors={true} />	<!-- App.svelte gets access and can change the properties below -->
<script>
	import { createEventDispatcher } from 'svelte';
	import { fade } from 'svelte/transition';

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

{#if !hidden}
	<li in:fade out:fade class:completed class:hidden>
		Task {num}: {description} - Due on {dueDate}
		<input type="checkbox" bind:checked={completed} />
		<button on:click="{() => dispatch('remove', null)}">Remove</button>
	</li>	
{/if}
