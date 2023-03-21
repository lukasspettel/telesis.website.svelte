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
			<item
				style=" background-color: rgba(255, 255, 255, 0.5); border-left:5px solid var({item.expand
					.category.color}); padding-left: 2rem">
				<a href={`/projects/${item.slug}`}
					><div>
						<h2 style="margin:0rem; color: var({item.expand.category.color})">{item.title}</h2>
						<flex-row style="padding-bottom:1rem">
							<a href={`/categories/${item.expand.category.slug}`}
								><h4 style="font-size: 1rem; color: var({item.expand.category.color});margin:0rem">
									{item.expand.category.title}
								</h4></a>
							<Time timestamp={item.date} />
						</flex-row>

						<flex-row style="gap:2rem">
							<img src={getImageURL(item.collectionId, item.id, item.image)} alt={item.title} />
						</flex-row>
					</div>
				</a>
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
