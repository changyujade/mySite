<script lang="ts">
	import { page } from '$app/state';
	import './layout.css';
	import '../app.css';

	let { children } = $props();

	const navItems = [
		{ href: '/', label: 'Home' },
		{ href: '/about', label: 'About' },
		{ href: '/projects', label: 'Projects' },
		{ href: '/weather', label: 'Weather' },
		{ href: '/contact', label: 'Contact' },
		{ href: '/cv.pdf', label: 'CV', external: true },
		{ href: 'https://medium.com/@chang.j0918', label: 'Medium', external: true }
	];
</script>

{#if page.url.pathname !== '/'}
	<nav class="site-nav" aria-label="Main navigation">
		<div class="nav-inner">
			<a href="/" class="site-title" aria-label="Jade Chang home">
				<span class="mark">JC</span>
				<span>Jade Chang</span>
			</a>

			<div class="nav-links">
				{#each navItems as item}
					<a href={item.href} target={item.external ? '_blank' : undefined}>{item.label}</a>
				{/each}
			</div>
		</div>
	</nav>
{/if}

<main>{@render children()}</main>
