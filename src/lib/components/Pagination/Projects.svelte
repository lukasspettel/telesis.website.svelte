<script>
	// @ts-nocheck
	import { getImageURL } from '$lib/utils/getURL'
	import Time from 'svelte-time'
	export let projects
	export let projectItemWidth
	export let category
</script>

<project-flex {projects} style="--item-width: {projectItemWidth}" {category}>
	{#each projects.items as item}
		{#if category === item.expand.category.title}
			<item
				style=" background-color: rgba(255, 255, 255, 0.5); border-left:5px solid var({item.expand
					.category.color}); padding-left: 2rem">
				<div>
					<flex-row>
						<a href={`/projects/${item.slug}`}
							><h2 style="margin:0rem; color: var({item.expand.category.color})">
								{item.title}
							</h2></a>
					</flex-row>

					<flex-row style="padding-bottom:1rem">
						<a href={`/categories/${item.expand.category.slug}`}
							><h4 style="font-size: 1rem; color: var({item.expand.category.color});margin:0rem">
								{item.expand.category.title}
							</h4></a>

					</flex-row>
					<div class="time"><Time timestamp={item.date}/></div>
					<flex-row style="gap:2rem">

						<a class="a-exclude" href={`/projects/${item.slug}`}>
							<img src={getImageURL(item.collectionId, item.id, item.image)} alt={item.title} /></a>
					</flex-row>
				</div>
			</item>
		{/if}
	{/each}
</project-flex>

<style>
	project-flex {
		padding-bottom: 2.5rem;
		display: flex;
		flex-wrap: wrap;
		grid-gap: 2.5rem;
	}

	project-flex item {
		width: var(--item-width);
		flex-grow: 1;
		white-space: wrap;
	}
	.time {
		font-family: 'Urbanist';
		font-size: 0.8rem;
	}

	h2 {
		margin-bottom: 1.5rem;
	}
	img {
		object-fit: cover;
		width: 100%;
		height: 50vh;
	}
	.a-exclude {
		width: 100%;
		height: 100%;
		box-shadow: none;
	}
</style>
