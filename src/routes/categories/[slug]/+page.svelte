<script>
	import { pbStore, Record } from 'svelte-pocketbase'
	import { getImageURL } from '$lib/utils/getURL'
	import Time from 'svelte-time'
	import { page } from '$app/stores'

	const categories = $pbStore.collection('categories').getList(1, 250, {
		sort: '-created'
	})
</script>

<content-container>
	<background style="background-image: url('{bgImage}')" />
	{#await categories}
		<div>Loading...</div>
	{:then categories}
		{#each categories.items as item}
			{#if item.slug === $page.params.slug}
				<div>
					<h2>{item.title}</h2>
					<p>{item.description}</p>
					<richtext-container>
						{@html item.body}
					</richtext-container>
				</div>
			{/if}
		{/each}
	{/await}
</content-container>
