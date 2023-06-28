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
</script>

{#await projects}
	<div>loading</div>
{:then projects}
	{#each projects.items as item}
		{#if item.slug === $page.params.slug}
			<img
				class="hero-img"
				src={getImageURL(item.collectionId, item.id, item.image)}
				alt={item.title} />
			<content-container>
				<div style="width:100%;">
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
					</flex-row>
					<h3><Time timestamp={item.date} /></h3>
					<p>{item.description}...</p>
				</div>
				<div style="padding-top:2rem; padding-bottom:1rem">
					{@html item.body}
				</div>
				{#if item.expand.company}
					<div style="padding-top:1rem; padding-bottom:1rem; width:100%">
						<flex-row style="gap:1rem">
							<a href="/collaborations/"><h1 style="margin:0;padding:0">Collaborations</h1></a>
						</flex-row>
						<div style="padding-top:1rem; padding-bottom:5rem; width:100%">
							<div style="border-top:5px solid var({item.expand.category.color});width:100%" />
							<companies-flex style="padding-top:2rem">
								{#each item.expand.company as item}
									<item>
										<a class="a-override" href={`${item.homepage}`}
											><img
												class="img-override"
												src={getImageURL(item.collectionId, item.id, item.logo)}
												alt={item.title} /></a>
									</item>
								{/each}
							</companies-flex>
						</div>
					</div>
				{/if}
				{#if item.expand.team}
					<flex-row style="gap:1rem">
						<a href="/team/"><h1 style="margin:0;padding:0">Team</h1></a>
					</flex-row>
					<div style="padding-top:1rem; padding-bottom:5rem; width:100%">
						<div style="border-top:5px solid var({item.expand.category.color});width:100%" />
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
				<Projects {projects} width={'100%'} category={item.expand.category.title} />
			</content-container>
		{/if}
	{/each}
{/await}

<style>
	a{
		padding: 0;
	}
	img {
		object-fit: cover;
	}
	.contact-img {
		object-fit: cover;
		width: 100%;
		height: 100%;
		max-height: 250px;
		max-width: 250px;
	}
	.hero-img {
		width: 100%;
		height: 100vh;
		object-fit: cover;
	}
	h1 {
		font-size: 3rem;
		padding: 0rem;
	}
	.a-override:hover {
		box-shadow: none;
	}
	h3 {
		padding-bottom: 0rem;
		margin-bottom: 2rem;
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
		align-items: center;
		justify-content: space-between;
		gap: 1rem;
	}

	team-flex item {
		white-space: wrap;
		border-radius: var(--element-border-radius);
	}

	img {
		height: fit-content;
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

	@media (min-width: 768px) and (max-width: 1200px) {
		team-flex item {
			width: 45%;
			height: 100%;
		}
		h1 {
			font-size: 2.5rem;
			margin-bottom: 2.5rem;
		}
	}
	@media (min-width: 480px) and (max-width: 768px) {
		team-flex item {
			width: 100%;
			height: 100%;
		}
		h1 {
			font-size: 2.5rem;
			margin-bottom: 2.5rem;
		}
	}
	@media (max-width: 480px) {
		team-flex item {
			width: 100%;
			height: 100%;
		}
		h1 {
			font-size: 2rem;
			margin-bottom: 2.5rem;
		}
	}
</style>
