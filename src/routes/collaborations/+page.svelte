<script>
	import { pbStore, Record } from 'svelte-pocketbase'
	import { getImageURL } from '$lib/utils/getURL'
	import Time from 'svelte-time'
	import { page } from '$app/stores'
	import Companies from '$lib/components/Sections/Companies.svelte'

	const companies = $pbStore.collection('companies').getList(1, 250, {
		sort: '-created'
	})

	let itemWidth = '25%'
</script>

<content-container>
	{#await companies}
		<div>loading</div>
	{:then companies}
		<Companies {companies} {itemWidth} />
	{/await}
</content-container>

<style>
	content-container {
		padding-top: 5rem;
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		padding-left: 10rem;
		padding-right: 10rem;
	}
</style>
