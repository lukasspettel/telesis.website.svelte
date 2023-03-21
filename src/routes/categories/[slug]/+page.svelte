<script>
	import { pbStore, Record } from 'svelte-pocketbase'
	import { getImageURL } from '$lib/utils/getURL'
	import Time from 'svelte-time'
	import { page } from '$app/stores'
	import Projects from '$lib/components/Pagination/Projects.svelte'

	const categories = $pbStore.collection('categories').getList(1, 250, {
		sort: '-created'
	})
	const projects = $pbStore.collection('projects').getList(1, 250, {
		sort: '-created',
		expand: 'category'
	})
	let projectItemWidth = '25%'
</script>

<content-container>
	{#await categories}
		<div>Loading...</div>
	{:then categories}
		{#each categories.items as item}
			{#if item.slug === $page.params.slug}
				<div style="padding-bottom:2rem">
					<div style="padding-bottom:3rem">
						<a href="/categories/">
							<h1 style="color: var({item.color});justify-content:flex-start">{item.title}</h1></a>
					</div>
					<div style="padding-bottom:4rem">
						<img src={getImageURL(item.collectionId, item.id, item.image)} alt={item.title} />
					</div>
					<p>{item.description}</p>
				</div>
				{#await projects}
					<div>Loading...</div>
				{:then projects}
					<div style="padding-bottom:2rem">
						<Projects {projects} {projectItemWidth} category={item.title} />
					</div>
				{/await}
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
	a {
		text-decoration: none;
	}
</style>
