<script>
	import { pbStore, Record } from 'svelte-pocketbase'
	import { getImageURL } from '$lib/utils/getURL'
	import MediaQuery from 'svelte-media-query'
	import Time from 'svelte-time'
	import News from '$lib/components/Sections/News.svelte'
	import Category from '$lib/components/Sections/Category.svelte'
	import Projects from '$lib/components/Sections/Projects.svelte'
	import Companies from '$lib/components/Sections/Companies.svelte'

	const news = $pbStore.collection('news').getList(1, 3, {
		sort: '-date'
	})

	const projects = $pbStore.collection('projects').getList(1, 9, {
		sort: '-date',
		expand: 'category'
	})

	const companies = $pbStore.collection('companies').getList(1, 250, {
		sort: '-created'
	})

	const categories = $pbStore.collection('categories').getList(1, 250, {
		sort: '-created'
	})
	const newsItemWidth = '30%'
	const projectItemWidth = '100%'
	const collaborationItemWidth = '10%'
</script>

<content-container>
	<Record collection="users" id="hm269p75apytq3g" let:record>
		<hero>
			<MediaQuery query="(min-width: 768px)" let:matches>
				{#if matches}
					<div>
						<img
							style="padding-bottom: 2rem; height: 200px;"
							src={record.logo ? getImageURL(record.collectionId, record.id, record.logo) : '/'}
							alt={record.title} />
						<h2 style="white-space: nowrap">{record.subheadline}</h2>
					</div>
				{/if}
			</MediaQuery>
			<MediaQuery query="(min-width: 480px) and (max-width: 768px)" let:matches>
				{#if matches}
					<div>
						<img
							style="padding-bottom: 2rem; height: 100px;"
							src={record.logo ? getImageURL(record.collectionId, record.id, record.logo) : '/'}
							alt={record.title} />
						<h2 style="white-space: wrap;font-size:1.2rem">{record.subheadline}</h2>
					</div>
				{/if}
			</MediaQuery>
			<MediaQuery query="(max-width: 480px)" let:matches>
				{#if matches}
					<div>
						<img
							style="padding-bottom: 1rem; height: 75px;"
							src={record.logo ? getImageURL(record.collectionId, record.id, record.logo) : '/'}
							alt={record.title} />
						<h2 style="white-space: wrap;font-size:1.2rem">{record.subheadline}</h2>
					</div>
				{/if}
			</MediaQuery>
		</hero>
	</Record>

	<!-- Categories Section Grid -->
	<category-flex>
		{#await categories}
			<div>loading</div>
		{:then category}
		<MediaQuery query="(min-width: 1200px)" let:matches>
			{#if matches}
			<Category {category} width={"45%"} subheadline={true} subheadlineCharacters={200} />
			{/if}
		</MediaQuery>
		<MediaQuery query="(min-width: 768px) and (max-width: 1200px)" let:matches>
			{#if matches}
			<Category {category} width={"100%"} subheadline={true} subheadlineCharacters={150} />
			{/if}
		</MediaQuery>
		<MediaQuery query="(min-width: 480px) and (max-width: 768px)" let:matches>
			{#if matches}
			<Category {category} width={"100%"} subheadline={false} subheadlineCharacters={100} />
			{/if}
		</MediaQuery>
		<MediaQuery query="(max-width: 480px)" let:matches>
			{#if matches}
			<Category {category} width={"100%"} subheadline={false} subheadlineCharacters={100} />
			{/if}
		</MediaQuery>

		{/await}
	</category-flex>

	<!-- <flex-row style="gap: 1rem;padding-bottom:2rem"
		><a href="/news/"><h1>Updates & News</h1></a></flex-row>
	{#await news}
		<div>loading</div>
	{:then news}
		<News {news} {newsItemWidth} />
	{/await} -->

	<flex-row style="gap: 1rem;padding-bottom:2rem"
		><a href="/projects/"><h1>Projects</h1></a>
	</flex-row>

	{#await projects}
		<div>loading</div>
	{:then projects}
		<Projects {projects} width={"25%"} />
	{/await}

	<flex-row style="gap: 1rem;padding-bottom:2rem"
		><a href="/collaborations/"><h1>Collaborations</h1></a>
	</flex-row>
	{#await companies}
		<div>loading</div>
	{:then companies}
		<Companies {companies} {collaborationItemWidth} />
	{/await}
</content-container>

<style>
	hero {
		margin: auto;
		align-items: center;
		justify-content: center;
		width: 100%;
		height: 100vh;
		display: flex;
		flex-direction: column;
	}

	h1 {
		font-size: 2.5rem;
		margin-bottom: 0rem;
	}
	h2 {
		font-size: 1.8rem;
		margin-bottom: 0rem;
	}


	@media (min-width: 768px) and (max-width: 1200px) {

	}
	@media (min-width: 480px) and (max-width: 768px) {

	}
	@media (max-width: 480px) {

	}
</style>
