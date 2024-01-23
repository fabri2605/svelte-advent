<script>
	import { onMount } from 'svelte';

	let childrenList = [];
	let childrenCharged = [];
	let total = 0;

	const fetcher = async () => {
		const response = await fetch('https://advent.sveltesociety.dev/data/2023/day-three.json');
		await response.json().then((e) => (childrenList = e));
	};

	const onClick = (e) => {
		console.log(e);
		childrenCharged = [...childrenCharged, e];
		total = total + e.weight;
	};

	onMount(() => fetcher());
</script>

<h1>Actions</h1>
<div id="actions">
	<h2>Total: {total} kilograms</h2>
	{#if childrenCharged.length}
		<div class="boys">
			{#each childrenCharged as boy}
				<p>{boy.name} charged {boy.weight} kg</p>
			{/each}
		</div>
	{/if}
</div>
<button on:click={() => (childrenCharged = [])}>Clear</button>

{#if childrenList.length > 0}
	<h1>Children and weights</h1>
	<div id="kids">
		{#each childrenList as c}
			<button
				disabled={childrenCharged.find((e)=>e.name === c.name && e.weight === c.weight).length>0}
				class="lekids"
				on:click={() => onClick(c)}
			>
				<p>{c.name}</p>
				<p>{c.weight}</p>
			</button>
		{/each}
	</div>
{:else}
	<div>
		<h1>Loading..</h1>
	</div>
{/if}

<style>
	#kids {
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: center;
		align-items: center;
		gap: 100px;
		text-align: center;
		width: 90vh;
	}

	.lekids {
		background-color: rgb(55, 5, 102);
		border-radius: 20px;
		width: 85px;
		height: 95px;
		border: grey solid 1px;
	}
	.lekids:disabled {
		background-color: rgba(221, 213, 230, 0.744);
		border-radius: 20px;
		width: 85px;
		height: 95px;
		border: grey solid 1px;
	}
	p {
		color: white;
	}
	.boys {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: flex-start;
		margin: 0;
		background-color: rgb(4, 4, 86);
		border-radius: 10px;
		width: 300px;
		padding: 0 20px;
		margin: 20px;
	}
	#actions {
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: center;
		gap: 100px;
	}
</style>
