<script>
	import Time from 'svelte-time'
	import { getImageURL } from '$lib/utils/getURL'
	export let category
	export let categoryItemWidth
</script>

<category-flex {category} style="--item-width: {categoryItemWidth}">
	{#each category.items as item}
		<item>
			<div style="position:relative; border-radius: var(--element-border-radius);">
				<div
					style="border-radius: var(--element-border-radius);z-index:-2;width: 100%; height: 100%; position: absolute; background-color: var(--white-cuba);" />
				<div
					style="opacity: 0.15; width: 100%; height: 100%; z-index:-1; position:absolute; padding: 2rem; background-size: cover; background-image: url('{getImageURL(
						item.collectionId,
						item.id,
						item.background_image
					)}')" />
				<div style="padding: 2.5rem">
					<h3>{item.title}</h3>
					<p>{item.description.slice(0, 300)}...</p>
					<a style="font-weight:bold;color:var({item.color})" href={`/categories/${item.slug}`}
						>Read more...</a>
				</div>
			</div>
			<!-- <img
						src={getImageURL(item.collectionId, item.id, item.background_image)}
						alt={item.title}
					/> -->
		</item>
	{/each}
</category-flex>

<style>
	category-flex {
		padding-bottom: 2.5rem;
		display: flex;
		flex-wrap: wrap;
		grid-gap: 2.5rem;
	}

	category-flex item {
		width: var(--item-width);
		flex-grow: 1;
		white-space: wrap;
		border-radius: var(--element-border-radius);
	}

	category-flex item p {
		font-size: 1rem;
		color: var(--black-suite);
	}
</style>
