<script>
	import { pbStore, Record } from 'svelte-pocketbase'
	import { getImageURL } from '$lib/utils/getURL'
	import Time from 'svelte-time'
	import { page } from '$app/stores'
	import Projects from '$lib/components/Pagination/Projects.svelte'

	const projects = $pbStore.collection('projects').getList(1, 250, {
		sort: '-created',
		expand: 'companies, category'
	})
	let projectItemWidth = '25%'
</script>

{#await projects}
	<div>loading</div>
{:then projects}
	{#each projects.items as item}
		{#if item.slug === $page.params.slug}
			<img src={getImageURL(item.collectionId, item.id, item.image)} alt={item.title} />
			<content-container>
				<div>
					<div>
						<flex-row>
							<h1>{item.title}</h1>
							<h4>{item.expand.category.title}</h4>
							<h4><Time timestamp={item.date} /></h4>
						</flex-row>
						<p>{item.description}...</p>
					</div>
				</div>
				<div>
					{@html item.body}
				</div>
				<Projects {projects} {projectItemWidth} category={item.expand.category.title} />
			</content-container>
		{/if}
	{/each}
{/await}

<style>
	img {
		object-fit: cover;
		width: 100vw;
		height: 100vh;
	}
</style>
