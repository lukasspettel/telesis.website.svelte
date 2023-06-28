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

<content-container style="padding-bottom:5rem">
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
						<div>
							<img
							class="contact-img "
								src={getImageURL(item.collectionId, item.id, item.image)}
								alt={item.name} />
							<h3>{item.name}</h3>
							<h6>{item.role}</h6>
							<p>+{item.phone}</p>
							<a href={`mailto:${item.email}`}><p>{item.email}</p></a>
							<a href={`${item.homepage}`}> <p>{item.homepage}</p></a>
						</div>
					</item>
				{/if}
			{/each}
		</team-flex>
		<h2>Externe</h2>
		<team-flex>
			{#each team.items as item}
				{#if !item.intern}
					<item>
						<div>
							<img
								class="contact-img "
								src={getImageURL(item.collectionId, item.id, item.image)}
								alt={item.name} />
							<h3>{item.name}</h3>
							<h6>{item.role}</h6>
							<p>+{item.phone}</p>
							<a href={`mailto:${item.email}`}><p>{item.email}</p></a>
							<a href={`${item.homepage}`}><p>{item.homepage}</p></a>
						</div>
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
		justify-content: space-between;
		gap: 2.5rem;
		padding-bottom: 2rem;
	}

	team-flex item {
		justify-content: space-between;
		flex-grow: 1;
		white-space: wrap;
		border-radius: var(--element-border-radius);
	}

	.contact-img {
		object-fit: cover;
		width: 250px;
		height: 250px;
		max-height: 250px;
		max-width: 250px;
	}

	a {
		padding: 0;
		margin: 0;
	}

	p {
		font-size: 0.8rem;
		margin: 0;
		padding: 0;

	}

	h1 {
		padding-top: 5rem;
		font-size: 4rem;
		margin-bottom: 0rem;
	}

	h2 {
		font-size: 3rem;
		margin-bottom: 0.5rem;
		
	}

	img {
		border-radius: var(--element-border-radius);
	}

	h3 {
		margin: 0;
		padding: 0;
		margin: 0;
	}
	h4 {
		margin: 0;
	}
	h6 {
		padding: 0;
		margin: 0;
	}
	
	@media (min-width: 768px) and (max-width: 1200px) {
		team-flex item {
			width: 45%;
			height: 100%;
		}
		h1 {
			font-size: 4rem;
		}
	}
	@media (min-width: 480px) and (max-width: 768px) {
		team-flex item {
			width: 100%;
			height: 100%;
		}
		h1 {
			font-size: 3rem;
		}
	}
	@media (max-width: 480px) {
		team-flex item {
			width: 100%;
			height: 100%;
		}
		h1 {
			font-size: 2rem;
		}
	}
</style>
