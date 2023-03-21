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
		expand: 'category,company,team'
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
				<div style="padding-top:5rem; width:100%;">
					<flex-row>
						<a href="/"
							><h1 style="color:var({item.expand.category.color});justify-content:flex-start">
								{item.title}
							</h1></a>
					</flex-row>
					<flex-row>
						<a href={`/categories/${item.expand.category.slug}`}
							><h3 style="color:var({item.expand.category.color})">
								{item.expand.category.title}
							</h3></a>
						<h3><Time timestamp={item.date} /></h3></flex-row>

					<p>{item.description}...</p>
				</div>
				<div style="padding-top:2rem; padding-bottom:1rem">
					{@html item.body}
				</div>
				{#if item.expand.company}
					<div style="padding-top:1rem; padding-bottom:1rem; width:100%">
						<flex-row style="gap:1rem;justify-content:flex-start">
							<a href="/collaborations/"><h1 style="margin-bottom:1rem">Collaborationen</h1></a>
						</flex-row>
						<div style="border-top:5px solid var({item.expand.category.color});width:100%" />
						<companies-flex style="padding-top:2rem">
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
					</div>
				{/if}
				{#if item.expand.team}
					<div style="padding-top:1rem; padding-bottom:5rem; width:100%">
						<flex-row style="gap:1rem;justify-content:flex-start">
							<a href="/team/"><h1 style="margin-bottom:1rem">Team</h1></a>
						</flex-row>
						<div style="border-top:5px solid var({item.expand.category.color});width:100%" />
						<team-flex style="padding-top:2rem">
							{#each item.expand.team as item}
								<item>
									<flex-row>
										<div style="width:150px;height:150px">
											<img
												style="object-fit: cover; width: 100%;height: 100%;"
												src={getImageURL(item.collectionId, item.id, item.image)}
												alt={item.name} />
										</div>
										<div>
											<h4>{item.name}</h4>
											<h6>{item.role}</h6>
										</div>
									</flex-row>
								</item>
							{/each}
						</team-flex>
					</div>
				{/if}
				<div style="padding-bottom:2rem">
					<a href={`/categories/${item.expand.category.slug}`}
						><h3 style="color:var({item.expand.category.color})">
							{item.expand.category.title}
						</h3></a>
					<Projects {projects} {projectItemWidth} category={item.expand.category.title} />
				</div>
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
	team-flex {
		display: flex;
		flex-wrap: wrap;
		gap: 1rem;
	}

	team-flex item {
		width: 25%;
		height: 25%;
		align-items: flex-start;
		justify-content: flex-start;
		white-space: wrap;
		flex-grow: 1;
		border-radius: var(--element-border-radius);
	}

	team-flex flex-row {
		align-items: flex-start;
		justify-content: flex-start;
		gap: 1rem;
	}
	img {
		border-radius: var(--element-border-radius);
	}
	h4 {
		font-size: 0.9rem;
		margin: 0;
	}
	h6 {
		font-size: 0.8rem;
		margin: 0;
	}
</style>
