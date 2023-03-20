<script>
	import { pbStore, Record } from 'svelte-pocketbase'
	import { page } from '$app/stores'
	import bgImage from '$lib/assets/images/background/Topographic Map Patterns_4.svg'

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
				<h2>{item.title}</h2>
				<div>
					{@html item.body}
				</div>
			{/if}
		{/each}
	{/await}
</content-container>
