<script>
	import { pbStore, Record } from 'svelte-pocketbase'
	import { getImageURL } from '$lib/utils/getURL'
	import Time from 'svelte-time'
	import News from '$lib/components/Sections/News.svelte'
	import Category from '$lib/components/Sections/Category.svelte'
	import Projects from '$lib/components/Sections/Projects.svelte'
	import Companies from '$lib/components/Sections/Companies.svelte'
	import bgImage from '$lib/assets/images/background/Topographic Map Patterns.svg'

	const news = $pbStore.collection('news').getList(1, 6, {
		sort: '-date'
	})

	const projects = $pbStore.collection('projects').getList(1, 6, {
		sort: '-date',
		expand: 'category, company'
	})

	const companies = $pbStore.collection('companies').getList(1, 250, {
		sort: '-created'
	})

	const categories = $pbStore.collection('categories').getList(1, 250, {
		sort: '-created'
	})

	const categoryItemWidth = '45%'
	const newsItemWidth = '20%'
</script>

<content-container>
	<Record collection="users" id="hm269p75apytq3g" let:record>
		<background style="background-image: url('{bgImage}')" />
		<hero>
			<img
				style="padding-bottom: 2rem; width: 800px;"
				src={record.logo ? getImageURL(record.collectionId, record.id, record.logo) : '/'}
				alt={record.title} />
			<h2>{record.subheadline}</h2>
		</hero>
	</Record>

	<!-- Categories Section Grid -->
	<category-flex>
		{#await categories}
			<div>loading</div>
		{:then category}
			<Category {category} {categoryItemWidth} />
		{/await}
	</category-flex>

	<flex-row style="gap: 1rem;"
		><h1>Updates & News</h1>
		<a href="/news/"><p style="font-size:0.75rem;">View All</p></a>
	</flex-row>
	{#await news}
		<div>loading</div>
	{:then news}
		<News {news} {newsItemWidth} />
	{/await}

	<flex-row style="gap: 1rem"
		><h1>Projects</h1>
		<a href="/projects/"><p style="font-size:0.75rem;">View All</p></a>
	</flex-row>

	{#await projects}
		<div>loading</div>
	{:then projects}
		<Projects {projects} />
	{/await}

	<flex-row style="gap: 1rem"
		><h1>Collaborations</h1>
		<a href="/collaborations/"><p style="font-size:0.75rem;">View All</p></a>
	</flex-row>
	{#await companies}
		<div>loading</div>
	{:then companies}
		<Companies {companies} />
	{/await}
</content-container>

<style>
	hero {
		margin: auto;
		padding-top: 5rem;
		padding-bottom: 5rem;
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	a {
		text-decoration: none;
	}

	h1 {
		font-size: 2.5rem;
		margin-bottom: 0rem;
	}
	h2 {
		font-size: 3rem;
		margin-bottom: 0rem;
	}
</style>
