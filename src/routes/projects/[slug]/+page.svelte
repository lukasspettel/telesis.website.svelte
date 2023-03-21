<script>
	import { pbStore, Record } from 'svelte-pocketbase'
	import { getImageURL } from '$lib/utils/getURL'
	import Time from 'svelte-time'
	import { page } from '$app/stores'
	import Projects from '$lib/components/Pagination/Projects.svelte'
	import Companies from '$lib/components/Sections/Companies.svelte'

	const categories = $pbStore.collection('categories').getList(1, 250, {
		sort: '-created'
	})
	const projects = $pbStore.collection('projects').getList(1, 250, {
		sort: '-created',
		expand: 'category,company'
	})
	let projectItemWidth = '25%'
	let collaborationItemWidth = '10%'
</script>

{#await projects}
	<div>loading</div>
{:then projects}
	{#each projects.items as item}
		{#if item.slug === $page.params.slug}
			<img src={getImageURL(item.collectionId, item.id, item.image)} alt={item.title} />
			<content-container>
				<div style="padding-top:5rem">
					<h1>{item.title}</h1>
					<flex-row>
						<h4>{item.expand.category.title}</h4>
						<h4><Time timestamp={item.date} /></h4></flex-row>

					<p>{item.description}...</p>
				</div>
				<div>
					{@html item.body}
				</div>

				{#if item.expand.company}
					<flex-row style="gap:1rem">
						<h1>Collaborationen</h1>
						<a href="/collaborations/"><p style="font-size:0.75rem;">View All</p></a>
					</flex-row>
					<companies-flex>
						{#each item.expand.company as item}
							<item>
								<a href={`${item.homepage}`}
									><img
										class="img-override"
										src={getImageURL(item.collectionId, item.id, item.logo)}
										alt={item.title} /></a>
							</item>
						{/each}
					</companies-flex>
				{/if}
				<Projects {projects} {projectItemWidth} category={item.expand.category.title} />
			</content-container>
		{/if}
	{/each}
{/await}

<style>
	img {
		object-fit: cover;
	}
	h1 {
		font-size: 3rem;
		margin-bottom: 2.5rem;
	}
	companies-flex {
		padding-bottom: 2.5rem;
		display: flex;
		flex-wrap: wrap;
		grid-gap: 2.5rem;
	}

	companies-flex item {
		width: 200px;
		flex-grow: 1;
		white-space: wrap;
		border-radius: var(--element-border-radius);
	}
</style>
