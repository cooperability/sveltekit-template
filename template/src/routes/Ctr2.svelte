<script lang="ts">
	import { countStore } from './store';
	let count = 0;
	export let myProps = {
		name: 'cooper',
		project: 'svelte',
		day: 8.26
	};
	const items = [
		{ id: 1, name: 'one' },
		{ id: 2, name: 'two' },
		{ id: 3, name: 'three' }
	];
	function addOne() {
		count += 1;
	}
	$: document.title = `count is ${count}`;
	$: doubled = count * 2;
	const promise = Promise.resolve(69);
</script>

<button on:click={addOne}
	>Clicked {count} times. Double that is {doubled} My name is {myProps.name}.</button
>
<button on:click={() => countStore.update((c) => (c += 1))}
	>Clicked {$countStore} times. This number is in separate storage.</button
>
{#if count > 1000}
	<p>big</p>
{:else if count > 5}
	<p>medium</p>
{:else}
	<p>small</p>
{/if}

{#each items as item (item.id)}
	<p>{item.name}</p>
{/each}

{#await promise}
	<!-- render loading gif -->
{:then number}
	<p>{document.title}</p>
{:catch error}
	<!-- error -->
{/await}
