<script>
	import logo from '$lib/assets/images/Telesis_Logo_black_nospace.svg'
</script>

<div>
	<nav>
		<ul>
			<a href="/"><img src={logo} /></a>
		</ul>
		<ul>
			<li><a href="/categories">Categories</a></li>
			<li><a href="/projects">Projects</a></li>
			<li><a href="/news">News</a></li>
			<li><a href="/collaborations">Collaboration</a></li>
			<li><a href="/team">Team</a></li>
			<li><a href="/contact">Contact</a></li>
		</ul>
	</nav>
</div>

<style>
	nav {
		padding-left: 2rem;
		padding-right: 2rem;
		box-shadow: 0px 1px 5px 0px rgba(0, 0, 0, 0.1);
		background-color: white;
	}

	img {
		width: 150px;
	}

	a {
		font-family: 'urbanist';
		color: var(--black-suite);
		text-decoration: none;
	}
</style>
