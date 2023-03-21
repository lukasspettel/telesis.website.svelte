<script>
	import Time from 'svelte-time'
	import { getImageURL } from '$lib/utils/getURL'

	export let category
	export let categoryItemWidth
</script>

<category-flex {category} style="--item-width: {categoryItemWidth}">
	{#each category.items as item}
		<item>
			<a href={`/categories/${item.slug}`}>
				<div style="position:relative; border-radius: var(--element-border-radius)">
					<div
						style="border-radius: var(--element-border-radius);z-index:-2;width: 100%; height: 100%; position: absolute; background-color: var(--white-cuba);" />
					<div
						style=" background-image: url('{getImageURL(
							item.collectionId,
							item.id,
							item.background_image
						)}')" />
					<div style="padding: 2.5rem; justify-content:stretch;height:100%;">
						<h1 style="color:var({item.color})">{item.title}</h1>
						<p>{item.description.slice(0, 300)}...</p>
					</div>
				</div>
			</a>
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
		height: 100%;
		flex-grow: 1;
		white-space: wrap;
		border-radius: var(--element-border-radius);
	}

	category-flex item p {
		font-size: 0.9rem;
		color: var(--black-suite);
	}

	a {
		text-decoration: none;
	}
	h1 {
		font-size: 2rem;
	}
</style>
