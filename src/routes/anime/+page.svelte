<script>
	import ImageGallery from '../../components/ImageGallery.svelte';
	import Navbar from '../../components/Navbar.svelte';
	import Footer from '../../components/Footer.svelte';
</script>

<main>
	<Navbar />
	<div class="container">
		<div class="sv-page-wrapper">
			<ImageGallery />
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
