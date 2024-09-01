<script>
	import { onMount } from 'svelte';

	let sidenavInstance;

	onMount(() => {
		const elems = document.querySelectorAll('.sidenav');
		sidenavInstance = M.Sidenav.init(elems, {});
	});

	function openSidenav() {
		if (sidenavInstance && sidenavInstance.length > 0) {
			sidenavInstance[0].open();
		}
	}

	function closeSidenav() {
		if (sidenavInstance && sidenavInstance.length > 0) {
			sidenavInstance[0].close();
		}
	}
</script>

<div class="sv-nav-wrapper">
	<!-- Navbar -->
	<nav>
		<div class="container">
			<div class="nav-wrapper">
				<a href="/" class="brand-logo left">SANIME</a>
				<ul id="nav-mobile" class="right hide-on-med-and-down">
					<li><a href="https://jozbiz.com/#" target="_blank">By JB Sandbox</a></li>
				</ul>
				<a href="#" data-target="slide-out" class="sidenav-trigger right">
					<i class="material-icons">menu</i>
				</a>
			</div>
		</div>
	</nav>

	<!-- Sidenav -->
	<ul id="slide-out" class="sidenav">
		<li>
			<div class="user-view">
				<div class="background">
					<img src="sidenav-bg.jpg" alt="header-bg" />
				</div>
				<a href="#name"><span class="white-text name">SANIME</span></a>
				<a href="#email"><span class="white-text email">Anime community</span></a>
			</div>
		</li>
		<li>
			<a href="/about" class="sidenav-link" on:click|capture|nonpassive={closeSidenav}>
				<i class="material-icons">info</i>About
			</a>
		</li>
	</ul>
</div>

<style>
	nav {
		background-color: #5853b2;
	}
	.sidenav .user-view {
		min-height: 160px;
	}
	.sidenav .user-view .background img {
		width: 100%;
	}
</style>
