<script>
	import { getImageURL } from '$lib/utils/getURL'
	import Time from 'svelte-time'
	export let projects
	export let projectItemWidth
	export let category
</script>

<project-flex {projects} style="--item-width: {projectItemWidth}" {category}>
	{#each projects.items as item}
		{#if category === item.expand.category.title}
			<item style=" background-color: rgba(255, 255, 255, 0.5);">
				<div>
					<flex-row
						><a href={`/projects/${item.slug}`}><h2 style="margin:0rem">{item.title}</h2></a>
						<Time timestamp={item.date} />
					</flex-row>
					<flex-row style="gap:2rem">
						<img src={getImageURL(item.collectionId, item.id, item.image)} />
					</flex-row>
				</div>
			</item>
		{/if}
	{/each}
</project-flex>

<style>
	a {
		text-decoration: none;
		color: var(--black-suite);
	}
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
		border-radius: var(--element-border-radius);
	}

	h2 {
		margin-bottom: 1.5rem;
	}
	img {
		object-fit: cover;
		width: 100%;
		height: 50vh;
	}
</style>
