<script>
	import CategoriesGallery from '../components/CategoriesGallery.svelte';
	import Navbar from '../components/Navbar.svelte';
	import Footer from '../components/Footer.svelte';
</script>

<main>
	<Navbar />
	<div class="minh-vh container">
		<div class="sv-page-wrapper">
			<CategoriesGallery />
		</div>
	</div>
	<Footer />
</main>

<style>
	.sv-page-wrapper {
		padding: 24px 0;
	}
</style>
