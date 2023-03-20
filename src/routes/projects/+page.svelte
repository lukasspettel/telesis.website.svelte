<script>
	import { pbStore, Record } from 'svelte-pocketbase'
	import { getImageURL } from '$lib/utils/getURL'
	import Time from 'svelte-time'
	import { page } from '$app/stores'
	import Projects from '$lib/components/Sections/Projects.svelte'

	const projects = $pbStore.collection('projects').getList(1, 250, {
		sort: '-created',
		expand: 'category'
	})

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
				<h1>
					<div>Projects</div>
				</h1>
				<richtext-container>
					{@html item.body}
				</richtext-container>
			{/if}
		{/each}
	{/await}
	{#await projects}
		<div>Loading...</div>
	{:then projects}
		<Projects {projects} />
	{/await}
</content-container>

<style>
	h1 {
		padding-top: 5rem;
		font-size: 4rem;
		margin-bottom: 0rem;
	}
</style>
