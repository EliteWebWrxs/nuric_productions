<script>
	let { data, children } = $props();
	import { page } from '$app/state';
	import '$lib/css/reset.css';
	import '$lib/css/styles.css';
	import logo from '$lib/images/logo.webp';

	let menuOpen = $state(false);
	$effect(() => {
		const mobileMenu = document.getElementById('mobileMenu');
		if (mobileMenu instanceof HTMLElement) {
			mobileMenu.addEventListener('toggle', (e) => {
				menuOpen = mobileMenu.matches(':popover-open');
			});
		}
	});

	// add class to body based on pathname strip the / remove all other classes
	$effect(() => {
		if (data.pathname.replace('/', '') === '') {
			document.body.classList.remove(
				...Array.from(document?.body?.classList).filter(
					(className) => className !== data.pathname.replace('/', '')
				)
			);
			document.body.classList.add('home');
		} else {
			document.body.classList.add(data.pathname.replace('/', ''));
			document.body.classList.remove(
				...Array.from(document?.body?.classList).filter(
					(className) => className !== data.pathname.replace('/', '')
				)
			);
		}
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

	const currentPath = $derived(page.url.pathname);

	function closeMenu() {
		const menu = document.getElementById('mobileMenu');
		if (menu instanceof HTMLElement) {
			menu.hidePopover();
		}
	}
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
	<nav class="desktopNav">
		<ul>
			{#each routes as route}
				<li><a href={route.href}>{route.label}</a></li>
			{/each}
		</ul>
	</nav>
	<nav class="mobileNav">
		<button class="hamburger" class:menuOpen popovertarget="mobileMenu" aria-label="Toggle menu">
			<div class="line line1"></div>
			<div class="line line2"></div>
			<div class="line line3"></div>
		</button>
	</nav>
	<dialog class="mobileMenu" popover="auto" id="mobileMenu">
		<ul>
			<li class={page.href === currentPath ? 'active' : ''}>
				<a href="/">Home</a>
			</li>
			{#each routes as page}
				<li class={page.href === currentPath ? 'active' : ''}>
					<a href={page.href} onclick={closeMenu}>{page.label}</a>
				</li>
			{/each}
		</ul>
	</dialog>
</header>

<div>
	{@render children()}
</div>

<footer>
	<div class="footerContainer">
		<div class="footerContent">
			<div class="facebookLinkContainer">
				<div class="facebookLink">
					<a href="http://facebook.com/Nuricproductions" target="_blank">
						<span class="visuallyHidden">Facebook</span>
						<svg viewBox="0 0 173 323" fill="none" xmlns="http://www.w3.org/2000/svg">
							<path
								d="M161.778 178.555L170.667 123H117.334V84.1107C117.334 68.5551 122.889 56.3329 147.334 56.3329H172.889V5.22179C158.445 2.99957 142.889 0.777344 128.445 0.777344C82.8892 0.777344 50.667 28.5551 50.667 78.5551V123H0.666992V178.555H50.667V319.666C61.7781 321.889 72.8892 323 84.0003 323C95.1114 323 106.223 321.889 117.334 319.666V178.555H161.778Z"
								fill="white"
							/>
						</svg>
					</a>
				</div>
			</div>
			<div class="footerCopyright">
				<p class="footerCopyrightText">
					&copy; {new Date().getFullYear()} Nuric Productions. All rights reserved.
				</p>
			</div>
		</div>
	</div>
</footer>

<style>
	header {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 0 2rem;
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
	.facebookLinkContainer {
		display: flex;
		justify-content: center;
		align-items: center;
		margin: 0;
	}
	.facebookLink {
		width: 50px;
		height: 50px;
		border: 3px solid #fff;
		border-radius: 50%;
		display: flex;
		justify-content: center;
		align-items: center;
		svg {
			width: 25px;
			height: 25px;
		}
	}
	.visuallyHidden {
		position: absolute;
		width: 1px;
		height: 1px;
		padding: 0;
		margin: -1px;
		overflow: hidden;
		clip: rect(0, 0, 0, 0);
		white-space: nowrap;
		border: 0;
	}
	.footerContent {
		width: calc(100% - 4rem);
		max-width: 1600px;
		margin: 0 auto;
		display: flex;
		justify-content: space-between;
		align-items: center;
	}
	.footerCopyrightText {
		font-size: 0.9rem;
		margin: 0;
	}
	.desktopNav {
		display: block;
	}
	.mobileNav {
		display: none;
	}
	@media (max-width: 768px) {
		.mobileNav {
			display: block;
		}
		.desktopNav {
			display: none;
		}
	}
	.hamburger {
		width: 24px;
		height: 24px;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		transition: transform 0.3s ease;
	}
	button {
		background: none;
		border: none;
		padding: 0;
		margin: 0;
		cursor: pointer;
	}

	.line {
		width: 100%;
		height: 2px;
		background-color: #fff;
		transition: all 0.3s ease;
	}

	.menuOpen {
		.line1 {
			transform: rotate(45deg) translate(6px, 7px);
		}

		.line2 {
			opacity: 0;
		}

		.line3 {
			transform: rotate(-45deg) translate(8px, -10px);
		}
	}

	.mobileMenu {
		transition:
			scale 0.5s ease,
			opacity 0.5s ease,
			display 0.5s ease;
		opacity: 0;
		scale: 0.5;
		border: none;
		padding: 2rem;
		background-color: #333;
		border-radius: 1rem;
		transition-behavior: allow-discrete;
		@starting-style {
			opacity: 1;
			scale: 1;
		}
		ul {
			margin: 0;
			padding: 0;
			list-style: none;
		}
		li {
			width: 100%;
			text-align: center;
			padding: 1rem 0;
			border-bottom: 1px solid #333;
			font-size: 2rem;
			color: #fff;
			a {
				color: inherit;
				text-decoration: none;
			}
		}
	}

	.mobileMenu:popover-open {
		border: none;
		padding: 2rem;
		background-color: #333;
		border-radius: 1rem;
		overflow: auto;
		width: fit-content;
		opacity: 1;
		scale: 1;

		transition-behavior: allow-discrete;
		@starting-style {
			opacity: 0;
			scale: 0.5;
		}

		ul {
			margin: 0;
			padding: 0;
		}
		li {
			width: 100%;
			text-align: center;
			padding: 1rem 0;
			border-bottom: 1px solid #333;
			font-size: 2rem;
			color: #fff;
			a {
				color: inherit;
				text-decoration: none;
			}
		}
		&::backdrop {
			background-color: rgba(0, 0, 0, 0.5);
		}
	}
</style>
