<script lang="ts">
	import { onMount } from 'svelte';
	import axios from 'axios';

	let images = [];
	let observer;
	const smallerWidthLgAnimes = ['neko', 'waifu', 'husbando', 'kitsune'];
	let animeTypeValue = '';
	let imagesLoaded = false;

	let isClicked = false;
	let isReady = true;
	let progress = 0;
	let interval;

	function reloadPage() {
		isClicked = true;
		interval = setInterval(() => {
			progress += 100 / 5; // Update progress bar every second
			if (progress >= 100) {
				clearInterval(interval);
				location.reload();
			}
		}, 1000); // Update every second

		setTimeout(() => {
			isReady = true;
		}, 5000); // 5 seconds to enable button
	}

	// Function to load images from an API
	async function loadImages() {
		imagesLoaded = false;
		try {
			const queryString = window.location.search;
			const urlParams = new URLSearchParams(queryString);
			animeTypeValue = urlParams.get('type');
			if (animeTypeValue) {
				const response = await axios.get(`https://nekos.best/api/v2/${animeTypeValue}?amount=20`);
				images = response?.data?.results;
				imagesLoaded = true;
			}
		} catch (error) {
			console.error('Error fetching images:', error);
			imagesLoaded = true;
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
	{#if imagesLoaded}
		<div>
			<div class="flex-row page-title">
				<h5 class="text-ucase">{animeTypeValue}</h5>
				<button class="reload-button" on:click={reloadPage} disabled={isClicked || !isReady}>
					{#if isClicked}
						In {5 - Math.floor((progress / 100) * 5)}s...
					{:else}
						Reload
					{/if}
					<div class="progress-bar" style="width: {progress}%;"></div>
				</button>
			</div>
			<div class="row flex-row">
				{#each images as image}
					<div
						class={`col ${smallerWidthLgAnimes.includes(animeTypeValue) ? 'l3' : 'l6'} m6 s12 image-block`}
					>
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
		margin-left: 0;
	}
	.image-block-img {
		width: 100%;
		height: 100%;
		object-fit: contain;
		padding: 0 8px;
		height: 300px;
		background-color: #f4f4f4;
	}
	@media only screen and (max-width: 900px) {
		.card .card-content {
			padding: 16px;
		}
	}

	.reload-button {
		position: relative;
		padding: 10px 20px;
		font-size: 16px;
		cursor: pointer;
		background-color: #5853b2;
		color: white;
		border: none;
		border-radius: 5px;
		transition: transform 0.3s ease-in-out;
		overflow: hidden;
		margin: auto 0 auto auto;
	}

	.reload-button:disabled {
		background-color: #888;
		cursor: not-allowed;
	}

	.progress-bar {
		position: absolute;
		bottom: 0;
		left: 0;
		height: 4px;
		background-color: #5853b2;
		transition: width 1s linear;
	}
</style>
