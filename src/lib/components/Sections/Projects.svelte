<script>
	import { getImageURL } from '$lib/utils/getURL'
	import Time from 'svelte-time'
	export let projects
	export let projectItemWidth
</script>

<project-flex {projects} style="--item-width: {projectItemWidth}">
	{#each projects.items as item}
		<item style=" background-color: rgba(255, 255, 255, 0.5);">
			<div>
				<a href={`/projects/${item.slug}`}><h2 style="margin:0rem">{item.title}</h2></a>
				<a href={`/categories/${item.expand.category.slug}`}
					><h4 style="font-size: 1rem; color: var({item.expand.category.color});margin:0rem">
						{item.expand.category.title}
					</h4></a>
				<Time timestamp={item.date} />
				<flex-row style="gap:2rem">
					<img src={getImageURL(item.collectionId, item.id, item.image)} />
				</flex-row>
			</div>
		</item>
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
