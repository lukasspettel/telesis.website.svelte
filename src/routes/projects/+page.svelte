<script>
	import { pbStore, Record } from 'svelte-pocketbase'
	import { getImageURL } from '$lib/utils/getURL'
	import Time from 'svelte-time'
	import { page } from '$app/stores'
	import Projects from '$lib/components/Sections/Projects.svelte'
	import MediaQuery from 'svelte-media-query'

	const projects = $pbStore.collection('projects').getList(1, 250, {
		sort: '-date',
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
				<h1>Projects</h1>
				<richtext-container>
					{@html item.body}
				</richtext-container>
			{/if}
		{/each}
	{/await}
	{#await projects}
		<div>Loading...</div>
	{:then projects}
		<MediaQuery query="(min-width: 1200px)" let:matches>
			{#if matches}
				<Projects {projects} width={'25%'} />
			{/if}
		</MediaQuery>
		<MediaQuery query="(min-width: 768px) and (max-width: 1200px)" let:matches>
			{#if matches}
				<Projects {projects} width={'45%'} />
			{/if}
		</MediaQuery>
		<MediaQuery query="(min-width: 480px) and (max-width: 768px)" let:matches>
			{#if matches}
				<Projects {projects} width={'100%'} />
			{/if}
		</MediaQuery>
		<MediaQuery query="(max-width: 480px)" let:matches>
			{#if matches}
				<Projects {projects} width={'100%'} />
			{/if}
		</MediaQuery>
	{/await}
</content-container>

<style>
	h1 {
		padding-top: 5rem;
		font-size: 4rem;
		margin-bottom: 0rem;
	}
</style>
