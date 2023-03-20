<script>
	import { pbStore, Record } from 'svelte-pocketbase'
	import { getImageURL } from '$lib/utils/getURL'
	import Time from 'svelte-time'
	import { page } from '$app/stores'
	import bgImage from '$lib/assets/images/background/Topographic Map Patterns_4.svg'

	const team = $pbStore.collection('team').getList(1, 250, {
		sort: '-created',
		expand: 'companies'
	})

	const pages = $pbStore.collection('pages').getList(1, 10, {
		sort: '-created'
	})
</script>

<content-container>
	<background style="background-image: url('{bgImage}')" />
	{#await pages}
		<div>Loading...</div>
	{:then pages}
		{#each pages.items as item}
			{#if `/${item.slug}` === $page.route.id}
				<h1>
					<div>Projects</div>
				</h1>
				<richtext-container>
					{@html item.body}
				</richtext-container>
			{/if}
		{/each}
	{/await}
	{#await team}
		<div>loading</div>
	{:then team}
		<h1>Internes Team</h1>
		<flex-row>
			{#each team.items as item}
				{#if item.intern}
					<div>
						<div>
							<img
								style="width:200px; height:200px; object-fit: cover"
								src={getImageURL(item.collectionId, item.id, item.image)}
								alt={item.name} />
							<div>
								<h3>{item.name}</h3>
								<h4>{item.role}</h4>
								<p>mail:{item.email}</p>
								<p>phone: {item.phone}</p>
								<p>hp: {item.homepage}</p>
							</div>
						</div>
					</div>
				{/if}
			{/each}
		</flex-row>
		<h1>Externes Team</h1>
		<flex-row>
			{#each team.items as item}
				{#if !item.intern}
					<div>
						<div>
							<img
								style="width:200px; height:200px;object-fit: cover"
								src={getImageURL(item.collectionId, item.id, item.image)}
								alt={item.name} />
						</div>
						<div>
							<h3>{item.name}</h3>
							<h4>{item.role}</h4>
							<p>mail:{item.email}</p>
							<p>phone: {item.phone}</p>
							<p>hp: {item.homepage}</p>
						</div>
					</div>
				{/if}
			{/each}
		</flex-row>
	{/await}
</content-container>

<style>
	content-container {
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		padding-left: 10rem;
		padding-right: 10rem;
	}

	p {
		font-size: 0.8rem;
		margin: 0;
	}

	flex-row {
		gap: 2.5rem;
	}
</style>
