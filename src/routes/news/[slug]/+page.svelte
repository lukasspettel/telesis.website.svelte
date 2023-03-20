<script>
	import { pbStore, Record } from 'svelte-pocketbase'
	import { getImageURL } from '$lib/utils/getURL'
	import Time from 'svelte-time'
	import { page } from '$app/stores'

	const news = $pbStore.collection('news').getList(1, 250, {
		sort: '-created'
	})
</script>

<content-container>
	{#await news}
		<div>Loading...</div>
	{:then news}
		{#each news.items as item}
			{#if item.slug === $page.params.slug}
				<div>
					<h2>{item.title}</h2>
					<p>{item.description}</p>
				</div>
			{/if}
		{/each}
	{/await}
</content-container>
