<script>
	import { onMount } from 'svelte';
	import axios from 'axios';

	let apiCategories = [];
	let categories = [];

	// Function to load images from an API
	async function loadCategories() {
		try {
			const response = await axios.get('https://nekos.best/api/v2/endpoints');
			apiCategories = response?.data;
			if (typeof apiCategories === 'object' && apiCategories !== null) {
				categories = Object.keys(apiCategories);
			}
		} catch (error) {
			console.error('Error fetching images:', error);
		}
	}

	// Load images when the component mounts
	onMount(() => {
		loadCategories();
	});
</script>

<div class="sv-img-list-wrap">
	<div class="row flex-row">
		{#each categories as category}
			<a href={`/anime/?type=${category}`} class="col s3 image-block">
				<div class="card">
					<!-- <div class="card-image">
						<img src={image.url} alt={image.artist_name} class="image-block-img" />
					</div> -->
					<div class="card-content">
						<p>
							{category || ''}
						</p>
					</div>
					<!-- <div class="card-action">
						<a href="#">This is a link</a>
					</div> -->
				</div>
			</a>
		{/each}
	</div>
</div>

<style>
	.flex-row {
		display: flex;
		flex-wrap: wrap;
	}
	.image-block {
		margin-bottom: 24px;
	}
</style>
