<script>
	import Footer from '$lib/components/Footer.svelte'
	import { pbStore } from 'svelte-pocketbase'
	import Navbar from '$lib/components/Navbar.svelte'
	import bgImage from '$lib/assets/images/background/Topographic Map Patterns.svg'

	pbStore.set('http://127.0.0.1:8090/')
</script>

<background style="background-image: url('{bgImage}')" />
<Navbar />
<div>
	<slot />
</div>
<Footer />

<style global>
	@import url('https://fonts.googleapis.com/css?family=Inter&display=swap');
	@import url('https://fonts.googleapis.com/css?family=Urbanist&display=swap');

	:root {
		--white-cuba: #e7e8e9;
		--black-suite: #2a2735;
		--grey-altona-100: #b9b7b7;
		--grey-altona: #888585;
		--grey-london: #464242;
		--orange-biz: #e0bbaf;
		--purple-sience: #a2a4ec;
		--yellow-insurance: #bbaf91;
		--green-school: #84a7aa;
		--red-minus: #c46a84;

		--element-border-radius: 0.5rem;
	}

	:global(p) {
		font-size: 1rem;
		font-family: 'Inter';
	}
	:global(h1) {
		font-family: 'Urbanist';
		margin: 0;
	}
	:global(h2) {
		font-family: 'Urbanist';
	}
	:global(h3) {
		font-family: 'Urbanist';
	}
	:global(h4) {
		font-family: 'Urbanist';
	}
	:global(h5) {
		font-family: 'Urbanist';
	}
	:global(h6) {
		font-family: 'Urbanist';
	}
	background {
		opacity: 0.1;
		width: 100%;
		height: 100%;
		z-index: -3;
		position: fixed;
		background-position: center;
		background-repeat: repeat;
		background-size: cover;
	}
	:global(content-container) {
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: flex-start;
		padding-left: 10rem;
		padding-right: 10rem;
	}

	:global(richtext-container) {
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
	}
	:global(flex-row) {
		display: flex;
		flex-direction: row;
		flex: 1;
		justify-content: space-between;
		align-items: baseline;
	}
	:global(img) {
		width: 100%;
		height: 100%;
		border-radius: var(--element-border-radius);
	}
	:global(.img-override) {
		border-radius: 0;
	}

	:global(a) {
		color: var(--black-suite);
		position: relative;
		text-decoration: none;
		color: inherit;
	}
</style>
