<script>
	import { pbStore, Record } from 'svelte-pocketbase'
	import { getImageURL } from '$lib/utils/getURL'
	import Time from 'svelte-time'
	import { page } from '$app/stores'
	import News from '$lib/components/Sections/News.svelte'

	const news = $pbStore.collection('news').getList(1, 4, {
		sort: '-created'
	})

	let newsItemWidth = '100%'
</script>

<content-container>
	{#await news}
		<div>Loading...</div>
	{:then news}
		{#each news.items as item}
			{#if item.slug === $page.params.slug}
				<div>
					<h1>{item.title}</h1>
					<img src={getImageURL(item.collectionId, item.id, item.image)} alt={item.title} />
					<richtext-container style="padding-top:4rem;padding-bottom:4rem">
						{@html item.body}
					</richtext-container>
				</div>
			{/if}
		{/each}
		<News {news} {newsItemWidth} />
	{/await}
</content-container>

<style>
	h1 {
		padding-top: 5rem;
		padding-bottom: 2rem;
		font-size: 4rem;
		margin-bottom: 0rem;
	}
	a {
		text-decoration: none;
	}
</style>
