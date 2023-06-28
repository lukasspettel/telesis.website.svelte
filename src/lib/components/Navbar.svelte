<script>
	import logo from '$lib/assets/images/Telesis_Logo_black_nospace.svg'
	import MediaQuery from 'svelte-media-query'
	import { fly, fade } from 'svelte/transition'
	import FaAlignJustify from 'svelte-icons/fa/FaAlignJustify.svelte'

	let isNavbarActive = false

	function ActivateNavbar() {
		isNavbarActive = !isNavbarActive
	}
</script>

<MediaQuery query="(min-width: 768px)" let:matches>
	{#if matches}<div>
			<nav>
				<ul>
					<a class="a-exclude" href="/"
						><img class="img-override" src={logo} alt="Telesis Logo" /></a>
				</ul>
				<ul>
					<li><a href="/categories">Service</a></li>
					<!-- <li><a href="/news">News</a></li> -->
					<li><a href="/projects">Projects</a></li>
					<li><a href="/collaborations">Collaboration</a></li>
					<li><a href="/team">Team</a></li>
					<li><a href="/contact">Contact</a></li>
				</ul>
			</nav>
		</div>{/if}
</MediaQuery>
<MediaQuery query="(min-width: 480px) and (max-width: 768px)" let:matches>
	{#if matches}
		<div>
			<nav>
				<ul>
					<a class="a-exclude" href="/"
						><img class="img-override" src={logo} alt="Telesis Logo" /></a>
				</ul>
				{#if !isNavbarActive}
					<button on:click={ActivateNavbar} class="button-closer">
						<div style="color:black">
							<FaAlignJustify />
						</div>
					</button>
				{/if}

				{#if isNavbarActive}
					<button
						class="button-fullscreen-background"
						on:click={ActivateNavbar}
						transition:fly={{ duration: 800, y: 800 }}>
						<flex>
							<navigation style="align-items: center;text-align:right">
								<a href="/"><h1>Home</h1></a>
								<p><a href="/categories"><h1>Services</h1></a></p>
								<!-- <p><a href="/news"><h1>News</h1></a></p> -->
								<p><a href="/projects"><h1>Projects</h1></a></p>
								<p><a href="/collaborations"><h1>Collaboration</h1></a></p>
								<p><a href="/team"><h1>Team</h1></a></p>
								<p><a href="/contact"><h1>Contact</h1></a></p>
							</navigation>
						</flex>
					</button>
				{/if}
			</nav>
		</div>
	{/if}
</MediaQuery>
<MediaQuery query="(max-width: 480px)" let:matches>
	{#if matches}
		<div>
			<nav>
				<ul>
					<a class="a-exclude" href="/"
						><img class="img-override" src={logo} alt="Telesis Logo" /></a>
				</ul>
				{#if !isNavbarActive}
					<button on:click={ActivateNavbar} class="button-closer">
						<div style="color:black">
							<FaAlignJustify />
						</div>
					</button>
				{/if}

				{#if isNavbarActive}
					<button
						class="button-fullscreen-background"
						on:click={ActivateNavbar}
						transition:fly={{ duration: 800, y: 800 }}>
						<flex>
							<navigation style="align-items: center;text-align:right">
								<a href="/"><h1>Home</h1></a>
								<p><a href="/categories"><h1>Services</h1></a></p>
								<!-- <p><a href="/news"><h1>News</h1></a></p> -->
								<p><a href="/projects"><h1>Projects</h1></a></p>
								<p><a href="/collaborations"><h1>Collaboration</h1></a></p>
								<p><a href="/team"><h1>Team</h1></a></p>
								<p><a href="/contact"><h1>Contact</h1></a></p>
							</navigation>
						</flex>
					</button>
				{/if}
			</nav>
		</div>
	{/if}
</MediaQuery>

<style>
	nav {
		position: fixed;
		top: 0;
		width: 100%;
		padding-left: 2rem;
		padding-right: 2rem;
		box-shadow: 0px 1px 5px 0px rgba(0, 0, 0, 0.1);
		background-color: white;
		z-index: 3;
		display: flex;
	}

	img {
		width: 150px;
		height: auto;
		flex-shrink: 0;
		flex-grow: 1;
		padding: 1rem;
	}

	a {
		font-family: 'urbanist';
		color: var(--black-suite);
		text-decoration: none;
		font-size: 0.8rem;
		border-radius: 0;
		margin-bottom: 1rem;
	}
	.a-exclude {
		box-shadow: none;
	}

	.button-closer {
		border: none;
		width: 64px;
		height: 64px;
		margin: auto 0;
		background-color: rgba(255, 255, 255);
	}
	.button-fullscreen-background {
		overflow: hidden;
		width: 100vw;
		height: 100vh;
		left:0;
		z-index: 10;
		position: fixed;
		border: none;
		background-color: rgba(255, 255, 255, 0.9);
	}

	img {
		width: 244px;
	}

	navigation {
		display: flex;
		flex-direction: column;
		flex-grow: 1;
		flex-shrink: 1;
		height: 100%;
		width: 100%;
		justify-content: center;
	}
</style>
