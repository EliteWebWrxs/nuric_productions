<script>
	let { data, children } = $props();
	import '$lib/css/reset.css';
	import '$lib/css/styles.css';
	import logo from '$lib/images/logo.webp';
</script>

<svelte:head>
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
	<link
		href="https://fonts.googleapis.com/css2?family=Dosis:wght@200..800&family=Roboto:ital,wdth,wght@0,75..100,100..900;1,75..100,100..900&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<header>
	<div class="logoContainer">
		<a href="/">
			<img src={logo} alt="logo" />
		</a>
	</div>
</header>

<div>
	{@render children()}
</div>

<style>
	header {
		padding: 2rem;
	}
	.logoContainer {
		width: 150px;
	}
</style>
