<script>
	import logo from '$lib/assets/images/Telesis_Logo_black_nospace.svg'
</script>

<footer>
	<flex-row>
		<div>
			<a href="/"><img class="img-override" src={logo} alt="Telesis Logo" /></a>
			<p style="margin-top: 1rem">Telesis Entwicklungs- und Management GmbH</p>
			<p>©2023 Telesis GmbH.</p>
			<p><a href="/tearms-of-service">Tearms of Service</a></p>
		</div>
		<div>
			<h6>Navigation</h6>
			<p><a href="/categories">Services</a></p>
			<p><a href="/news">News</a></p>
			<p><a href="/projects">Projects</a></p>
			<p><a href="/collaborations">Collaboration</a></p>
			<p><a href="/team">Team</a></p>
			<p><a href="/contact">Contact</a></p>
		</div>
		<div>
			<h6>Social</h6>
			<p><a href="/categories">Facebook</a></p>
			<p><a href="/news">Twitter</a></p>
			<p><a href="/projects">Instagram</a></p>
			<p><a href="/collaborations">Github</a></p>
		</div>
	</flex-row>
</footer>

<style>
	img {
		width: 300px;
	}
	footer {
		padding-top: 2rem;
		padding-bottom: 2rem;
		padding-left: 5rem;
		padding-right: 5rem;
		background-color: white;
		box-shadow: 0px -1px 5px 0px rgba(0, 0, 0, 0.1);
	}

	a {
		text-decoration: none;
		color: var(--black-suite);
		margin: 0;
		padding: 0;
	}

	p {
		margin: 0.25rem 0rem 0.25rem 0rem;
		font-size: 0.75rem;
	}
	flex-row {
		align-items: baseline;
		justify-content: space-between;
	}
</style>
