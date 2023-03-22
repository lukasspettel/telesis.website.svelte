<script>
	import { pbStore, Record } from 'svelte-pocketbase'
	import { getImageURL } from '$lib/utils/getURL'
	import Time from 'svelte-time'
	import News from '$lib/components/Sections/News.svelte'
	import Category from '$lib/components/Sections/Category.svelte'
	import Projects from '$lib/components/Sections/Projects.svelte'
	import Companies from '$lib/components/Sections/Companies.svelte'

	const news = $pbStore.collection('news').getList(1, 3, {
		sort: '-date'
	})

	const projects = $pbStore.collection('projects').getList(1, 3, {
		sort: '-date',
		expand: 'category'
	})

	const companies = $pbStore.collection('companies').getList(1, 250, {
		sort: '-created'
	})

	const categories = $pbStore.collection('categories').getList(1, 250, {
		sort: '-created'
	})

	const categoryItemWidth = '45%'
	const newsItemWidth = '30%'
	const projectItemWidth = '100%'
	const collaborationItemWidth = '10%'
</script>

<content-container>
	<Record collection="users" id="hm269p75apytq3g" let:record>
		<hero>
			<img
				style="padding-bottom: 2rem; width: 500px;"
				src={record.logo ? getImageURL(record.collectionId, record.id, record.logo) : '/'}
				alt={record.title} />
			<h2 style="white-space: nowrap;">{record.subheadline}</h2>
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

	<flex-row style="gap: 1rem;"><a href="/news/"><h1>Updates & News</h1></a> </flex-row>
	{#await news}
		<div>loading</div>
	{:then news}
		<News {news} {newsItemWidth} />
	{/await}

	<flex-row style="gap: 1rem"><a href="/projects/"><h1>Projects</h1></a> </flex-row>

	{#await projects}
		<div>loading</div>
	{:then projects}
		<Projects {projects} {projectItemWidth} />
	{/await}

	<flex-row style="gap: 1rem"><a href="/collaborations/"><h1>Collaborations</h1></a> </flex-row>
	{#await companies}
		<div>loading</div>
	{:then companies}
		<Companies {companies} {collaborationItemWidth} />
	{/await}
</content-container>

<style>
	hero {
		margin: auto;
		padding: 10rem;
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	h1 {
		font-size: 2.5rem;
		margin-bottom: 0rem;
	}
	h2 {
		font-size: 1.8rem;
		margin-bottom: 0rem;
	}
</style>
