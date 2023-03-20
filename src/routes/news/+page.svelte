<script>
	import { pbStore, Record } from 'svelte-pocketbase'
	import { getImageURL } from '$lib/utils/getURL'
	import Time from 'svelte-time'
	import { page } from '$app/stores'
	import News from '$lib/components/Sections/News.svelte'

	const news = $pbStore.collection('news').getList(1, 250, {
		sort: '-created'
	})
	const pages = $pbStore.collection('pages').getList(1, 10, {
		sort: '-created'
	})

	let newsItemWidth = '100%'
</script>

<content-container>
	<h1>Updates & News</h1>
	{#await pages}
		<div>Loading...</div>
	{:then pages}
		{#each pages.items as item}
			{#if `/${item.slug}` === $page.route.id}
				<richtext-container>
					{@html item.body}
				</richtext-container>
			{/if}
		{/each}
	{/await}
	{#await news}
		<div>Loading...</div>
	{:then news}
		<News {news} {newsItemWidth} />
	{/await}
</content-container>

<style>
	h1 {
		padding-top: 5rem;
		font-size: 4rem;
		margin-bottom: 0rem;
	}
</style>
