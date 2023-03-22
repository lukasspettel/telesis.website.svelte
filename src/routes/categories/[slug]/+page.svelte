<script>
	import { pbStore, Record } from 'svelte-pocketbase'
	import { getImageURL } from '$lib/utils/getURL'
	import Time from 'svelte-time'
	import { page } from '$app/stores'
	import Projects from '$lib/components/Pagination/Projects.svelte'

	const categories = $pbStore.collection('categories').getList(1, 250, {
		sort: '-created',
		expand: 'team'
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
				{#if item.expand.team}
					<div style="padding-top:1rem; padding-bottom:5rem; width:100%">
						<flex-row style="gap:1rem;justify-content:flex-start">
							<a href="/team/"><h1 style="margin-bottom:1rem">Team</h1></a>
						</flex-row>
						<div style="border-top:5px solid var({item.color});width:100%" />
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
				{#await projects}
					<div>Loading...</div>
				{:then projects}
					<div style="padding-bottom:2rem; width:100%">
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
</style>
