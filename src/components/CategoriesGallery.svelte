<script>
	import { onMount } from 'svelte';
	import axios from 'axios';

	let apiCategories = [];
	let categories = [];
	let categoriesLoaded = false;

	// Function to load images from an API
	async function loadCategories() {
		categoriesLoaded = false;
		try {
			const response = await axios.get('https://nekos.best/api/v2/endpoints');
			apiCategories = response?.data;
			if (typeof apiCategories === 'object' && apiCategories !== null) {
				categories = Object.keys(apiCategories);
			}
			categoriesLoaded = true;
		} catch (error) {
			console.error('Error fetching images:', error);
			categoriesLoaded = true;
		}
	}

	// Load images when the component mounts
	onMount(() => {
		loadCategories();
	});
</script>

<div class="sv-img-list-wrap">
	{#if categoriesLoaded}
		<div>
			<h5 class="page-title">{categories.length} categories to browse from:</h5>
			<div class="row flex-row">
				{#each categories as category}
					<a href={`/anime/?type=${category}`} class="col l3 m6 s6 image-block">
						<div class="card">
							<div class="card-content">
								<p class="card-title">
									{category || ''}
								</p>
							</div>
						</div>
					</a>
				{/each}
			</div>
		</div>
	{:else}
		<img class="page-loading-image" src="/loading.gif" alt="page-loader" />
	{/if}
</div>

<style>
	.flex-row {
		display: flex;
		flex-wrap: wrap;
	}
	.image-block {
		margin-bottom: 24px;
	}
	.card-title {
		text-transform: capitalize;
	}
	.page-title {
		padding: 6px 8px 12px;
	}
</style>
