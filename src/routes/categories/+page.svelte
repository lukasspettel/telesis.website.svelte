<script>
	import { pbStore, Record } from 'svelte-pocketbase'
	import { getImageURL } from '$lib/utils/getURL'
	import Time from 'svelte-time'
	import { page } from '$app/stores'
	import Category from '$lib/components/Sections/Category.svelte'
	import bgImage from '$lib/assets/images/background/Topographic Map Patterns_4.svg'

	const categories = $pbStore.collection('categories').getList(1, 250, {
		sort: '-created'
	})
	const pages = $pbStore.collection('pages').getList(1, 10, {
		sort: '-created'
	})

	const itemWidth = '100%'
</script>

<content-container>
	<background style="background-image: url('{bgImage}')" />
	{#await pages}
		<div>Loading...</div>
	{:then pages}
		{#each pages.items as item}
			{#if `/${item.slug}` === $page.route.id}
				<h1>
					<div>Our areas of Work</div>
				</h1>
				<richtext-container>
					{@html item.body}
				</richtext-container>
			{/if}
		{/each}
	{/await}
	{#await categories}
		<div>Loading...</div>
	{:then category}
		<Category {category} {itemWidth} />
	{/await}
</content-container>

<style>
	h1 {
		padding-top: 5rem;
		font-size: 4rem;
		margin-bottom: 0rem;
	}
</style>
