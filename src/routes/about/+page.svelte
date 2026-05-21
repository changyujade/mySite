<script>
	const timeline = [
		'University of Chicago · Digital Studies of Language, Culture, and History',
		'Colby College · Computer Science + Music and French and Francophone Studies',
		'Exchange study · Copenhagen DIS Program and University of Geneva',
		'C2 French certification · European language framework'
	];
</script>

<div class="page-shell">
	<section class="hero-panel">
		<h2>About</h2>
		<h1>Interdisciplinary by design.</h1>
		<div class="hero-summary">
			<p class="lead">
				I work where language, music, cultural study, and computational logic meet,
				turning interdisciplinary questions into clear research, tools, and digital
				experiences.
			</p>
			<div class="button-row">
				<a class="button" href="/projects">See the Work</a>
				<a class="button secondary" href="/contact">Start a Conversation</a>
			</div>
		</div>
	</section>

	<section class="profile-grid">
		<div class="surface-card narrative">
			<h2>Research Shape</h2>
			<p>
				I am currently studying Digital Studies of Language, Culture, and History at the
				University of Chicago. Before that, I graduated from Colby College with a combined
				background in Computer Science + Music and French and Francophone Studies.
			</p>
			<p>
				My computer science training includes Python, Java, data structures, data
				management, statistical analysis, visualization, and machine learning. I have built
				projects ranging from Dijkstra-style algorithms to CNN-based sound classification
				for Chinese musical instruments.
			</p>
			<p>
				Language study has been equally central. Exchange programs in Copenhagen and
				Geneva expanded my international perspective and deepened my French studies, which
				led to C2-level certification.
			</p>
		</div>

		<aside class="timeline">
			{#each timeline as item, index}
			<div class="timeline-item" style={`--delay: ${index * 120}ms`}>
					<span>{String(index + 1).padStart(2, '0')}</span>
					<p>{item}</p>
				</div>
			{/each}
		</aside>
	</section>

	<section>
		<div class="section-head">
			<div>
				<h2>Methods</h2>
				<h2>What I bring together</h2>
			</div>
			<p>
				A mix of programming, cultural interpretation, multilingual research, and careful
				attention to user experience.
			</p>
		</div>

		<div class="card-grid">
			<div class="surface-card">
				<h3>Computational Analysis</h3>
				<p>Python, Java, machine learning, data structures, statistical analysis, and visualization.</p>
			</div>
			<div class="surface-card">
				<h3>Language and Culture</h3>
				<p>French and Francophone studies, digital humanities, discourse analysis, and multilingual communication.</p>
			</div>
			<div class="surface-card">
				<h3>Music Technology</h3>
				<p>Sound classification, Max-based research assistance, motif generation, and jazz theory tools.</p>
			</div>
		</div>
	</section>
</div>

<style>
	.profile-grid {
		display: grid;
		grid-template-columns: minmax(0, 1.15fr) minmax(280px, 0.85fr);
		gap: clamp(48px, 8vw, 96px);
		align-items: start;
	}

	.narrative {
		background: transparent;
		color: #000000;
	}

	.narrative h2 {
		color: #000000;
	}

	:global(.hero-panel > h2:first-child),
	.section-head > div > h2:first-child {
		display: block;
		margin-bottom: 34px;
		padding-bottom: 14px;
		border-bottom: 2px solid #000000;
		font-size: clamp(2.8rem, 7vw, 6.6rem);
		font-weight: 900;
		line-height: 0.86;
		text-transform: uppercase;
	}

	:global(.hero-panel > h2:first-child:hover),
	.section-head > div > h2:first-child:hover {
		transform: translateY(-6px);
		text-shadow:
			-0.13em 0.1em 0 #8ee3d0,
			0.13em -0.1em 0 #f1c27d,
			-0.22em 0.18em 0 rgba(142, 227, 208, 0.72),
			0.22em -0.18em 0 rgba(241, 194, 125, 0.72);
	}

	:global(.hero-panel > h2:first-child:hover::after),
	.section-head > div > h2:first-child:hover::after {
		background: #8ee3d0;
		box-shadow: 0.6em -0.32em 0 #f1c27d;
	}

	.narrative p {
		max-width: 760px;
	}

	.timeline {
		display: grid;
		gap: 26px;
	}

	.timeline-item {
		display: grid;
		grid-template-columns: auto 1fr;
		gap: 22px;
		align-items: start;
		border: 0;
		border-top: 1px solid #000000;
		border-radius: 0;
		padding: 26px 0;
		background: transparent;
		color: #000000;
		box-shadow: none;
		animation: slide-up 560ms ease both;
		animation-delay: var(--delay);
		transition:
			transform 220ms ease,
			background 220ms ease;
	}

	.timeline-item:hover {
		transform: translateY(-3px);
		background: transparent;
	}

	.timeline-item span {
		color: #000000;
		font-family: var(--font-heading);
		font-size: 0.9rem;
		font-weight: 900;
		border-bottom: 0;
		line-height: 1.2;
	}

	.timeline-item p {
		margin: 0;
	}

	@keyframes slide-up {
		from {
			opacity: 0;
			transform: translateY(12px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}

	@media (max-width: 800px) {
		.profile-grid {
			grid-template-columns: 1fr;
		}
	}
</style>
