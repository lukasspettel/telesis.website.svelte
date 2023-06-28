<script>
	import { pbStore, Record } from 'svelte-pocketbase'
	import { getImageURL } from '$lib/utils/getURL'
	import Time from 'svelte-time'
	import { page } from '$app/stores'
	import Category from '$lib/components/Sections/Category.svelte'

	const categories = $pbStore.collection('categories').getList(1, 250, {
		sort: '-created'
	})
	const pages = $pbStore.collection('pages').getList(1, 10, {
		sort: '-created'
	})

	const categoryItemWidth = '100%'
</script>

<content-container>
	{#await pages}
		<div>Loading...</div>
	{:then pages}
		{#each pages.items as item}
			{#if `/${item.slug}` === $page.route.id}
				<h1>
					<div>Telesis means rethinking.</div>
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
		<div style="padding-bottom: 5rem;">
			<Category {category} width={"100%"} subheadline={true} subheadlineCharacters={250} />
		</div>
	{/await}
</content-container>

<style>
	h1 {
		padding-top: 5rem;
		font-size: 4rem;
		margin-bottom: 0rem;
	}
	h2 {
		font-size: 3rem;
	}
</style>
