<script>
	import Time from 'svelte-time'

	export let news
	export let newsItemWidth
</script>

<news-flex {news} style="--item-width: {newsItemWidth}">
	{#each news.items as item}
		<item>
			<div style="padding: 2rem">
				<flex-row>
					<a href={`/news/${item.slug}`}><h4>{item.title}</h4></a>
				</flex-row>
				<p>{item.description.slice(0, 100)}...</p>
				<flex-row
					><a href={`/news/${item.slug}`}>Read more...</a><Time timestamp={item.date} /></flex-row>
			</div>
		</item>
	{/each}
</news-flex>

<style>
	.a-exclude {
		width: 100%;
		height: 100%;
		box-shadow: none;
	}
	news-flex {
		padding-bottom: 2.5rem;
		display: flex;
		flex-wrap: wrap;
		grid-gap: 2.5rem;
	}

	news-flex item {
		width: var(--item-width);
		flex-grow: 1;
		white-space: wrap;
		background-color: rgba(255, 255, 255, 0.5);
		border: 1px solid var(--grey-altona-100);
		border-radius: var(--element-border-radius);
	}

	p {
		font-size: 0.8rem;
		color: var(--black-suite);
	}

	h4 {
		margin-bottom: 0.5rem;
	}
</style>
