<script>
	import { pbStore, Record } from 'svelte-pocketbase'
	import { page } from '$app/stores'

	const pages = $pbStore.collection('pages').getList(1, 10, {
		sort: '-created'
	})
</script>

<content-container>
	{#await pages}
		<div>Loading...</div>
	{:then pages}
		{#each pages.items as item}
			{#if `/${item.slug}` === $page.route.id}
				<h1>{item.title}</h1>
				<div>
					{@html item.body}
				</div>
			{/if}
		{/each}
	{/await}
</content-container>

<style>
	h1 {
		padding-top: 5rem;
		font-size: 4rem;
		margin-bottom: 0rem;
	}
</style>
