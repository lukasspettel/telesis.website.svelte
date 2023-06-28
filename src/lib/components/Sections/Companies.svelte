<script>
	// @ts-nocheck
	import { getImageURL } from '$lib/utils/getURL'
	export let companies
	export let collaborationItemWidth
</script>

<companies-flex {companies} style="--item-width: {collaborationItemWidth}">
	{#each companies.items as item}
		<item>
			<a class="a-exclude" href={`${item.homepage}`}
				><img
					class="img-override"
					src={getImageURL(item.collectionId, item.id, item.logo)}
					alt={item.title} /></a>
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
		height: fit-content;
	}
	.a-exclude {
		width: 100%;
		height: 100%;
		box-shadow: none;
	}
</style>
