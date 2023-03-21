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
				<div>
					<a href="/categories/"> <h1 style="color: var({item.color})">{item.title}</h1></a>
					<p>{item.description}</p>
					<richtext-container>
						{@html item.body}
					</richtext-container>
				</div>
				{#await projects}
					<div>Loading...</div>
				{:then projects}
					<Projects {projects} {projectItemWidth} category={item.title} />
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
