<script lang="ts">
	import { onMount } from 'svelte';
	import axios from 'axios';

	let images = [];
	let observer;

	// Function to load images from an API
	async function loadImages() {
		try {
			const queryString = window.location.search;
			const urlParams = new URLSearchParams(queryString);
			const animeTypeValue = urlParams.get('type');
			if (animeTypeValue) {
				const response = await axios.get(`https://nekos.best/api/v2/${animeTypeValue}?amount=20`);
				images = response?.data?.results;
			}
		} catch (error) {
			console.error('Error fetching images:', error);
		}
	}

	// Load images when the component mounts
	onMount(() => {
		loadImages();
	});

	function lazyLoad(node) {
		let observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						node.src = node.dataset.src;
						observer.unobserve(node);
					}
				});
			},
			{
				root: null, // Use the viewport as the root
				rootMargin: '0px', // No margin, load exactly when in view
				threshold: 0.1 // Load when 10% of the image is in view
			}
		);

		observer.observe(node);

		// Cleanup function
		return {
			destroy() {
				if (observer) {
					observer.unobserve(node);
				}
			}
		};
	}
</script>

<div class="sv-img-list-wrap">
	<div class="row flex-row">
		{#each images as image}
			<div class="col s3 image-block">
				<div class="card">
					<div class="card-image">
						<img
							class="image-block-img"
							use:lazyLoad
							data-src={image.url}
							alt={image.artist_name}
							src="/loading.gif"
						/>
					</div>
					<div class="card-content">
						<p>
							{image?.artist_name || image?.anime_name || ''}
						</p>
					</div>
					<!-- <div class="card-action">
						<a href="#">This is a link</a>
					</div> -->
				</div>
			</div>
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
	.image-block-img {
		width: 100%;
		height: 100%;
		object-fit: contain;
		padding: 0 8px;
		height: 300px;
		background-color: #f4f4f4;
	}
</style>
