<script>
	import { pbStore, Record } from 'svelte-pocketbase'
	import { getImageURL } from '$lib/utils/getURL'
	import Time from 'svelte-time'
	import { page } from '$app/stores'

	const team = $pbStore.collection('team').getList(1, 250, {
		sort: '-created',
		expand: 'companies'
	})
</script>

<content-container>
	{#await team}
		<div>loading</div>
	{:then team}
		{#each team.items as item}
			<img src={getImageURL(item.collectionId, item.id, item.image)} alt={item.name} />
			<div>
				{#if item.title}
					<div>
						<h3>{item.title} {item.name}</h3>
						<h4>{item.role}</h4>
					</div>
				{:else}
					<div>
						<h3>{item.name}</h3>
						<h4>{item.role}</h4>
					</div>
				{/if}
			</div>
		{/each}
	{/await}
</content-container>

<style>
	content-container {
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		padding-left: 10rem;
		padding-right: 10rem;
	}
</style>
