<script>
	import Time from 'svelte-time'
	import { getImageURL } from '$lib/utils/getURL'

	export let category
	export let categoryItemWidth
</script>

<category-flex {category} style="--item-width: {categoryItemWidth}">
	{#each category.items as item}
		<item>
			<div style="position:relative; border-radius: var(--element-border-radius)">
				<div
					style="opacity:.75;border-radius: var(--element-border-radius);z-index:-2;width: 100%; height: 100%; position: absolute; background-color: var(--black-suite);" />
				<div
					style=" background-image: url('{getImageURL(
						item.collectionId,
						item.id,
						item.background_image
					)}')" />
				<div style="padding: 2.5rem; height:100%;">
					<flex-row>
						<a href={`/categories/${item.slug}`}>
							<h1 style="color:var({item.color})">{item.title}</h1></a>
					</flex-row>
					<h6 style="color:var({item.color})">{item.description.slice(0, 200)}...</h6>
				</div>
			</div>
		</item>
	{/each}
</category-flex>

<style>
	category-flex {
		padding-bottom: 2.5rem;
		display: flex;
		flex-wrap: wrap;
		grid-gap: 2.5rem;
		align-items: stretch;
	}

	category-flex item {
		align-items: center;
		width: var(--item-width);
		height: 100%;
		flex-grow: 1;
		white-space: wrap;
		border-radius: var(--element-border-radius);
	}

	category-flex item p {
		font-size: 0.9rem;
		color: var(--black-suite);
	}

	h1 {
		font-size: 2rem;
		white-space: wrap;
		margin-bottom: 0;
	}
	.a-exclude {
		width: 100%;
		height: 100%;
		box-shadow: none;
	}
</style>
