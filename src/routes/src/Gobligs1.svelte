<script>
	import { onMount } from 'svelte';

	let name = '';
	let kids = [];
	let filteredKids = [];
	let loading = true;

	const fetcher = async () => {
		const data = await fetch('https://advent.sveltesociety.dev/data/2023/day-one.json');
		kids = await data.json();
		loading = false;
		console.log(kids);
	};

	const updateFilteredKids = () => {
		console.log('filtering!');
		filteredKids = name.length > 0 ? kids.filter((k) => k.name.includes(name)) : [];
	};

	$: updateFilteredKids();

	onMount(() => {
		fetcher();
	});
</script>

<section>
	<h1>Welcome to the advent of Sveltekit</h1>
	<h1>The problem of the goblings with the kids:</h1>
	<input
		type="text"
		value={name}
		on:input={(e) => {
			name = e.target.value;
			updateFilteredKids();
		}}
	/>
	{#if loading}
		<h1>Loading...</h1>
	{:else}
		<div>
			{#each filteredKids as kid}
				<h3>{kid.name} has {kid.tally} points</h3>
			{:else}
				{#if !name.length}
					<h1>Search for a kid!</h1>
				{:else}
					<h1>No kid named that way..</h1>
				{/if}
			{/each}
		</div>
		<h1>Heres a list of the kids</h1>
		<div id="allKids">
			{#each kids as kid}
				<p>{kid.name},</p>
			{/each}
		</div>
	{/if}
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	h1 {
		width: 100%;
	}

	#allKids {
		width: 90vh;
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: center;
		align-items: center;
	}
</style>
