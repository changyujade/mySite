<script>
	import { Github, Linkedin, Mail, Phone } from '@lucide/svelte';

	const links = [
		{ label: 'Email', value: 'jadechang@uchicago.edu', href: 'mailto:jadechang@uchicago.edu', icon: Mail },
		{ label: 'Phone', value: '207-855-1579', href: 'tel:2078551579', icon: Phone },
		{
			label: 'LinkedIn',
			value: 'jade-c-4ab612138',
			href: 'https://www.linkedin.com/in/jade-c-4ab612138/',
			icon: Linkedin
		},
		{ label: 'GitHub', value: 'changyujade', href: 'https://github.com/changyujade', icon: Github }
	];
</script>

<div class="page-shell">
	<section class="business-card" aria-label="Jade Chang contact card">
		<div class="card-top">
			<div>
				<p class="card-kicker">Yu-Chieh Jade Chang</p>
				<h2>Digital Studies · Language · Music Technology</h2>
			</div>
			<!-- <div class="monogram">JC</div> -->
			<img src="/jade.jpeg" alt="Jade Chang" class="square-image" />
		</div>

		<p class="card-note">
			University of Chicago researcher working across computational culture, multilingual
			study, and creative technical systems.
		</p>

		<div class="contact-infographic" aria-label="Contact options">
			{#each links as item}
				{@const Icon = item.icon}
				<a
					class="contact-node"
					href={item.href}
					target={item.href.startsWith('http') ? '_blank' : undefined}
				>
					<span class="node-icon" aria-hidden="true"><Icon size={34} strokeWidth={1.8} /></span>
					<span class="node-label">{item.label}</span>
					<strong>{item.value}</strong>
				</a>
			{/each}
		</div>
	</section>
</div>

<style>
	.business-card {
		position: relative;
		overflow: hidden;
		border: 0;
		border-top: 1px solid #000000;
		border-radius: 0;
		padding: clamp(44px, 7vw, 88px) 0;
		background: transparent;
		color: #000000;
		box-shadow: none;
	}

	.business-card::after {
		content: '';
		position: absolute;
		right: -80px;
		bottom: -80px;
		width: 220px;
		height: 220px;
		border: 1px solid #000000;
		border-radius: 999px;
		opacity: 0.12;
	}

	.card-top {
		position: relative;
		z-index: 1;
		display: flex;
		align-items: start;
		justify-content: space-between;
		gap: clamp(34px, 6vw, 72px);
	}

	.card-kicker {
		margin: 0 0 12px;
		font-family: var(--font-heading);
		font-size: clamp(1rem, 2vw, 1.4rem);
		font-weight: 850;
		text-transform: uppercase;
		letter-spacing: 0.08em;
	}

	.business-card h2 {
		max-width: 720px;
		color: #000000;
		font-size: clamp(2rem, 5vw, 4.2rem);
		line-height: 0.98;
	}

	.monogram {
		display: grid;
		width: clamp(86px, 12vw, 140px);
		aspect-ratio: 1;
		place-items: center;
		border: 1px solid #000000;
		border-radius: 0;
		font-family: var(--font-heading);
		font-size: clamp(1.6rem, 3vw, 3rem);
		font-weight: 900;
		flex: 0 0 auto;
	}

	.card-note {
		position: relative;
		z-index: 1;
		max-width: 660px;
		margin: 34px 0;
		color: #000000;
		font-size: 1.16rem;
		line-height: 1.65;
	}

	.contact-infographic {
		position: relative;
		z-index: 1;
		display: grid;
		grid-template-columns: repeat(4, minmax(0, 1fr));
		gap: clamp(18px, 3vw, 34px);
		margin-top: 48px;
	}

	.contact-node {
		position: relative;
		display: grid;
		align-content: space-between;
		min-height: 260px;
		border-top: 2px solid #000000;
		padding: 18px 0 0;
		color: #000000;
		transition:
			transform 220ms ease,
			text-shadow 220ms ease;
	}

	.contact-node::after {
		content: '';
		position: absolute;
		left: 0;
		top: -2px;
		width: 0;
		height: 2px;
		background: #8ee3d0;
		box-shadow: 18px -6px 0 #f1c27d;
		transition: width 220ms ease;
	}

	.contact-node:hover {
		transform: translateY(-6px);
		text-shadow:
			-0.05em 0.04em 0 #8ee3d0,
			0.05em -0.04em 0 #f1c27d;
	}

	.contact-node:hover::after {
		width: 100%;
	}

	.node-label {
		font-family: var(--font-heading);
		font-weight: 850;
		text-transform: uppercase;
		letter-spacing: 0.08em;
	}

	.node-icon {
		display: grid;
		width: clamp(64px, 8vw, 96px);
		aspect-ratio: 1;
		place-items: center;
		margin: 16px 0 42px;
		border: 1px solid #000000;
	}

	.node-label {
		font-size: clamp(1.25rem, 2.4vw, 2rem);
		line-height: 0.95;
	}

	.contact-node strong {
		overflow-wrap: anywhere;
		margin-top: 14px;
		font-size: clamp(0.98rem, 1.5vw, 1.2rem);
		font-weight: 600;
	}

	@media (max-width: 680px) {
		.card-top {
			display: grid;
		}

		.contact-infographic {
			grid-template-columns: 1fr;
		}

		.contact-node {
			min-height: auto;
			gap: 14px;
		}

		.node-icon {
			margin: 12px 0;
		}
	}
</style>
