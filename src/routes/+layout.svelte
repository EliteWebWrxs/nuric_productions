<script>
	let { data, children } = $props();
	import '$lib/css/reset.css';
	import '$lib/css/styles.css';
	import logo from '$lib/images/logo.webp';

	// add class to body based on pathname strip the / remove all other classes
	$effect(() => {
		document.body.classList.add(data.pathname.replace('/', ''));
		document.body.classList.remove(
			...document.body.classList
				.toArray()
				.filter((className) => className !== data.pathname.replace('/', ''))
		);
	});

	const routes = [
		{
			label: 'DJ Services',
			href: '/dj'
		},
		{
			label: 'Photo Booth',
			href: '/photobooth'
		},
		{
			label: 'Our Team',
			href: '/our-team'
		},
		{
			label: 'Contact Us',
			href: '/contact'
		}
	];
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
	<nav>
		<ul>
			{#each routes as route}
				<li><a href={route.href}>{route.label}</a></li>
			{/each}
		</ul>
	</nav>
</header>

<div>
	{@render children()}
</div>

<style>
	header {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 2rem;
	}
	.logoContainer {
		width: 150px;
	}
	nav {
		display: flex;
		justify-content: space-between;
		align-items: center;
		ul {
			display: flex;
			gap: 2rem;
			list-style: none;
			margin: 0;
			padding: 0;
			li {
				margin: 0;
				padding: 0;
				font-size: clamp(1.2rem, 2vw, 1.5rem);
				a {
					text-decoration: none;
					color: #fff;
				}
			}
		}
	}
</style>
