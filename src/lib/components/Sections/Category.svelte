
<script>
	// @ts-nocheck
	import Time from 'svelte-time'
	import { getImageURL } from '$lib/utils/getURL'

	export let category
	export let width
	export let subheadline
	export let subheadlineCharacters
</script>

<category-flex {category} style="--item-width: {width}">
	{#each category.items as item}
		<item>
			<card>
				<div class="height-container">
					<flex-row>
						<a href={`/categories/${item.slug}`}>
							<h1 style="color:var({item.color};">{item.title}</h1></a>
					</flex-row>
					{#if subheadline}
						<h6 style="color:var({item.color})">
							{item.description.slice(0, subheadlineCharacters)}...
						</h6>
					{/if}
				</div>
			</card>
		</item>
	{/each}
</category-flex>

<style>
	category-flex {
		padding-bottom: 10rem;
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

	category-flex item card {
		position: relative;
		border-radius: var(--element-border-radius);
	}


	.height-container {
		min-height: 250px;
	}
	category-flex item p {
		font-size: 0.9rem;
		color: var(--black-suite);
	}

	h1 {
		font-size: 2.5rem;
		white-space: wrap;
		margin-bottom: 0;
	}
	h6 {
		font-size: 1.25rem;
		text-align: justify;
	}
	.a-exclude {
		width: 100%;
		height: 100%;
		box-shadow: none;
	}
	@media (min-width: 768px) and (max-width: 1200px) {
		.height-container {
			min-height: 100%;
		}
	}
	@media (min-width: 480px) and (max-width: 768px) {
		.height-container {
			min-height: 100%;
		}
	}
	@media (max-width: 480px) {
		.height-container {
			min-height: 100%;
		}
	}
</style>
