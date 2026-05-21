<script>
	const benefits = [
		{
			title: 'Turn complex culture into readable evidence',
			copy:
				'I use computational methods to surface patterns in language, music, and digital communities without flattening the human questions behind them.'
		},
		{
			title: 'Build research that people can actually use',
			copy:
				'From misogyny analysis to jazz-learning tools, my work focuses on interfaces and explanations that make analysis approachable.'
		},
		{
			title: 'Move fluently across disciplines',
			copy:
				'Computer science, French and Francophone studies, music, and digital humanities shape how I ask questions and build answers.'
		}
	];
</script>

<div class="landing-shell">
	<section class="landing-hero">
		<div class="hero-copy">
			<h2>Yu-Chieh Jade Chang</h2>
			<a class="headline-link" href="/about" aria-label="Go to About page">
				<h1>Research-minded digital work for culture, language, and sound.</h1>
			</a>
			<p class="value-prop">
				I build clear, thoughtful digital projects that help people understand complex
				cultural patterns through code, design, and humanistic interpretation.
			</p>
			<div class="button-row">
				<a class="button" href="/projects">Explore Projects</a>
				<a class="button secondary" href="/about">Meet Jade</a>
			</div>
		</div>

		<a class="name-mark" href="/about" aria-label="Go to About page">
			<span>Jade</span>
			<span>Chang</span>
		</a>
	</section>

	<section class="benefit-grid" aria-label="Reasons to explore this site">
		{#each benefits as benefit}
			<a class="surface-card benefit-card" href="/projects">
				<h2>{benefit.title}</h2>
				<p>{benefit.copy}</p>
			</a>
		{/each}
	</section>

	<section class="site-cta">
		<div>
			<h2>Start with the work. Stay for the method.</h2>
			<p>
				See how technical systems, multilingual research, and cultural analysis come
				together across the portfolio.
			</p>
		</div>
		<a class="button" href="/projects">Read the Portfolio</a>
	</section>
</div>

<style>
	.landing-shell {
		display: grid;
		gap: 34px;
		animation: page-in 560ms ease both;
	}

	.landing-hero {
		display: grid;
		grid-template-columns: minmax(300px, 0.9fr) minmax(320px, 1.1fr);
		gap: clamp(28px, 5vw, 64px);
		align-items: center;
		min-height: calc(100vh - 210px);
		padding: clamp(28px, 5vw, 56px) 0;
	}

	.hero-copy {
		display: grid;
		align-content: center;
	}

	.hero-copy h1 {
		max-width: 720px;
		font-size: clamp(3rem, 7vw, 6.9rem);
		line-height: 0.94;
	}

	.headline-link {
		display: block;
		color: #000000;
		transition:
			transform 220ms ease,
			text-shadow 220ms ease;
	}

	.headline-link:hover {
		transform: translateY(-4px);
		text-shadow: 0 18px 54px rgba(0, 0, 0, 0.16);
	}

	.value-prop {
		max-width: 620px;
		margin: 26px 0 0;
		color: #000000;
		font-family: var(--font-reading);
		font-size: clamp(1.1rem, 2vw, 1.42rem);
		line-height: 1.68;
	}

	.name-mark {
		position: relative;
		display: grid;
		justify-self: end;
		color: #000000;
		font-family: var(--font-heading);
		font-size: clamp(4.5rem, 13vw, 12rem);
		font-weight: 800;
		line-height: 0.82;
		text-align: right;
		transition:
			transform 320ms ease,
			text-shadow 320ms ease;
	}

	.name-mark::before,
	.name-mark::after {
		content: 'Jade Chang';
		position: absolute;
		inset: 50% 0 auto auto;
		transform: translateY(-50%);
		opacity: 0;
		pointer-events: none;
		line-height: 0.82;
		transition:
			opacity 220ms ease,
			transform 320ms ease;
	}

	.name-mark::before {
		color: #8ee3d0;
		z-index: -1;
	}

	.name-mark::after {
		color: #f1c27d;
		z-index: -2;
	}

	.name-mark:hover {
		transform: translateY(-8px) scale(1.015);
		text-shadow: 0 26px 80px rgba(142, 227, 208, 0.28);
	}

	.name-mark:hover::before {
		opacity: 0.72;
		transform: translate(-12px, calc(-50% + 10px));
	}

	.name-mark:hover::after {
		opacity: 0.46;
		transform: translate(14px, calc(-50% - 12px));
	}

	.name-mark span {
		display: block;
	}

	.benefit-grid {
		display: grid;
		grid-template-columns: repeat(3, minmax(0, 1fr));
		gap: 16px;
	}

	.benefit-card h2 {
		font-size: clamp(1.35rem, 2.3vw, 2.05rem);
	}

	.benefit-card {
		border: 0;
		background: transparent;
		box-shadow: none;
		padding-inline: 0;
	}

	.benefit-card:hover {
		transform: translateY(-3px);
		background: transparent;
		box-shadow: none;
	}

	.site-cta {
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: 24px;
		padding: clamp(22px, 4vw, 34px);
	}

	.site-cta h2 {
		font-size: clamp(1.8rem, 3vw, 3rem);
	}

	.site-cta p {
		max-width: 620px;
		margin: 14px 0 0;
		color: #000000;
		font-family: var(--font-reading);
		font-size: 1.08rem;
		line-height: 1.65;
	}

	@media (max-width: 900px) {
		.landing-hero,
		.benefit-grid {
			grid-template-columns: 1fr;
		}

		.name-mark {
			justify-self: start;
			text-align: left;
		}

		.site-cta {
			align-items: flex-start;
			flex-direction: column;
		}
	}
</style>
