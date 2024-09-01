<script>
	import Navbar from '../../components/Navbar.svelte';
	import Footer from '../../components/Footer.svelte';
</script>

<main>
	<Navbar />
	<div class="container">
		<div class="sv-page-wrapper">
			<div class="about-section minh-vh">
				<h4>About This Gallery</h4>
				<p>
					Welcome to SANIME Gallery, a curated anime collection built from Safe for Work (SFW) sources.
					<br />
					This project was created as part of an ongoing experiment to develop an engaging anime community.
				</p>
				<p>
					Throughout this journey, we have explored numerous resources online that have been
					dedicated to processing and storing these assets over time. We may consider following a
					similar path in the future.
				</p>
				<p>
					As this project evolves, we plan to expand the gallery by adding more assets and
					introducing new features. These enhancements will be part of an upcoming freemium project,
					designed for anime enthusiasts who are eager to explore more.
				</p>
				<p>
					This gallery is a part of the web experiments conducted under <strong>JB Sandbox</strong>.
					We invite you to view the full collection <a href="https://jozbiz.com/" target="_blank">here</a>.
				</p>
			</div>
		</div>
	</div>
	<Footer />
</main>

<style>
	.sv-page-wrapper {
		padding: 24px 0;
	}
	@media only screen and (max-width: 900px) {
		.sv-page-wrapper {
			padding: 24px 0;
		}
	}
</style>
