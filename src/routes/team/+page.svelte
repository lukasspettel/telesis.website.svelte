<script>
	import { pbStore, Record } from 'svelte-pocketbase'
	import { getImageURL } from '$lib/utils/getURL'
	import Time from 'svelte-time'
	import { page } from '$app/stores'

	const team = $pbStore.collection('team').getList(1, 250, {
		sort: '-created',
		expand: 'companies'
	})

	const pages = $pbStore.collection('pages').getList(1, 10, {
		sort: '-created'
	})
</script>

<content-container>
	{#await pages}
		<div>Loading...</div>
	{:then pages}
		{#each pages.items as item}
			{#if `/${item.slug}` === $page.route.id}
				<h1>Telesis Team</h1>
				<richtext-container>
					{@html item.body}
				</richtext-container>
			{/if}
		{/each}
	{/await}
	{#await team}
		<div>loading</div>
	{:then team}
		<h2>Interne</h2>
		<team-flex>
			{#each team.items as item}
				{#if item.intern}
					<item>
						<flex-row>
							<div>
								<img
									style="object-fit: cover"
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
						</flex-row>
					</item>
				{/if}
			{/each}
		</team-flex>
		<h2>Externe</h2>
		<team-flex>
			{#each team.items as item}
				{#if !item.intern}
					<item>
						<flex-row>
							<div>
								<img
									style="object-fit: cover"
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
						</flex-row>
					</item>
				{/if}
			{/each}
		</team-flex>
	{/await}
</content-container>

<style>
	team-flex {
		display: flex;
		flex-wrap: wrap;
		gap: 2.5rem;
	}

	team-flex item {
		width: 40%;
		height: 100%;
		align-items: flex-start;
		justify-content: flex-start;
		flex-grow: 1;
		white-space: wrap;
		border-radius: var(--element-border-radius);
	}

	p {
		font-size: 0.8rem;
		margin: 0;
	}

	h1 {
		padding-top: 5rem;
		font-size: 4rem;
		margin-bottom: 0rem;
	}

	flex-row {
		align-items: flex-start;
		justify-content: flex-start;
		gap: 2.5rem;
	}
	img {
		border-radius: var(--element-border-radius);
	}
</style>
