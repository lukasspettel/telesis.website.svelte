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
</script>

<content-container>
	{#await categories}
		<div>Loading...</div>
	{:then categories}
		{#each categories.items as item}
			{#if item.slug === $page.params.slug}
				<div style="padding-bottom:2rem">
					<div style="padding-bottom:3rem">
						<a href="/categories/"> <h1 style="color: var({item.color})">{item.title}</h1></a>
					</div>
					<div style="padding-bottom:4rem">
						<img src={getImageURL(item.collectionId, item.id, item.image)} alt={item.title} />
					</div>
					<p>{item.description}</p>
				</div>
				{#if item.expand.team}
					<flex-row style="gap:1rem;">
						<a href="/team/"><h1 style="margin:0;padding:0">Team</h1></a>
					</flex-row>
					<div style="padding-top:1rem; padding-bottom:5rem; width:100%">
						<div style="border-top:5px solid var({item.color});width:100%" />
						<team-flex style="padding-top:2rem">
							{#each item.expand.team as item}
								<item>
									<div style="width:250px;height:250px">
										<img
											class="contact-img"
											src={getImageURL(item.collectionId, item.id, item.image)}
											alt={item.name} />
									</div>
									<h4>{item.name}</h4>
									<h6>{item.role}</h6>
								</item>
							{/each}
						</team-flex>
					</div>
				{/if}
				{#await projects}
					<div>Loading...</div>
				{:then projects}
					<div style="padding-bottom:2rem; width:100%">
						<Projects {projects} width={"25%"} category={item.title} />
					</div>
				{/await}
			{/if}
		{/each}
	{/await}
</content-container>

<style>
	.contact-img {
		object-fit: cover;
		width: 100%;
		height: 100%;
		max-height: 250px;
		max-width: 250px;
	}
	h1 {
		padding-top: 5rem;
		font-size: 4rem;
		margin-bottom: 0rem;
	}
	team-flex {
		display: flex;
		flex-wrap: wrap;
		align-items: center;
		justify-content: space-between;
		gap: 1rem;
	}

	team-flex item {
		white-space: wrap;
		border-radius: var(--element-border-radius);
	}

	team-flex flex-row {
		align-items: flex-start;
		justify-content: flex-start;
		gap: 1rem;
	}

	@media (min-width: 768px) and (max-width: 1200px) {
		team-flex item {
			width: 45%;
			height: 100%;
		}
		h1 {
			font-size: 4rem;
		}
	}
	@media (min-width: 480px) and (max-width: 768px) {
		team-flex item {
			width: 100%;
			height: 100%;
		}
		h1 {
			font-size: 3rem;
		}
	}
	@media (max-width: 480px) {
		team-flex item {
			width: 100%;
			height: 100%;
		}
		h1 {
			font-size: 2rem;
		}
	}
</style>
