<script>
	import { getImageURL } from '$lib/utils/getURL'
	import Time from 'svelte-time'
	export let projects
</script>

<project-flex {projects}>
	{#each projects.items as item}
		<item style=" background-color: rgba(255, 255, 255, 0.5);">
			<div style="padding: 2rem">
				<flex-row
					><a href={`/projects/${item.slug}`}><h2>{item.title}</h2></a>
					<a href={`/categories/${item.expand.category.slug}`}
						><h4 style="font-size: 1rem; color: var({item.expand.category.color})">
							{item.expand.category.title}
						</h4></a>
					<Time timestamp={item.date} />
				</flex-row>
				<flex-row style="gap:2rem">
					<div
						style="width: 100%; height:100%; min-height: 500px; color:white; margin: auto;border-radius: var(--element-border-radius); background-size: cover; background-image: url('{getImageURL(
							item.collectionId,
							item.id,
							item.image
						)}')" />
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
		width: 100%;
		flex-grow: 1;
		white-space: wrap;
		border-radius: var(--element-border-radius);
	}

	project-flex item .text-hover {
		padding: 2rem;
		opacity: 0;
		transition: opacity 0.3s ease-in-out;
		border-radius: var(--element-border-radius);
		background-color: rgba(37, 31, 31, 0.25);
	}

	p {
		font-size: 1.2rem;
		color: var(--white-cuba);
	}

	h2 {
		margin-bottom: 1.5rem;
	}

	hr {
		border-top: 2px solid var(--black-suite);
	}
</style>
