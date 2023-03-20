<script>
	import { getImageURL } from '$lib/utils/getURL'
	export let companies
	export let itemWidth
</script>

<companies-flex {companies} style="--item-width: {itemWidth}">
	{#each companies.items as item}
		<item>
			<a href={`${item.homepage}`}
				><img src={getImageURL(item.collectionId, item.id, item.logo)} alt={item.title} /></a>
		</item>
	{/each}
</companies-flex>

<style>
	companies-flex {
		padding-bottom: 2.5rem;
		display: flex;
		flex-wrap: wrap;
		grid-gap: 2.5rem;
	}

	companies-flex item {
		width: var(--item-width);
		flex-grow: 1;
		white-space: wrap;
		border-radius: var(--element-border-radius);
	}

	p {
		color: var(--black-suite);
	}

	img {
		position: relative;
		width: 260px;
		object-fit: cover;
	}
</style>
