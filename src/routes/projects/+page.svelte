<script>
	const profileUrl =
		'https://soundcloud.com/user-929081810?utm_source=clipboard&utm_medium=text&utm_campaign=social_sharing';
	const embedUrl = `https://w.soundcloud.com/player/?url=${encodeURIComponent(profileUrl)}&visual=true`;

	const projects = [
		{
			title: 'Misogyny Analysis on Threads',
			type: 'Digital humanities · Social media analysis',
			status: 'In progress',
			copy:
				'An analysis project examining misogynistic language, social patterns, and platform-specific discourse on Threads. The work brings together computational text analysis, interpretive humanities methods, and visual summaries that make harmful language patterns easier to investigate.',
			tags: ['NLP', 'social media', 'discourse analysis', 'ethics'],
			featured: true
		},
		{
			title: 'Jazz Analyzer',
			type: 'Music technology · Capstone',
			status: 'Built',
			href: 'https://github.com/changyujade/jazz-analyzer',
			copy:
				'A web tool for beginning jazz learners that parses chord data, normalizes songs into Roman numeral notation, identifies progressions, and explains chord functions with scale suggestions.',
			tags: ['Python', 'music theory', 'education', 'UX']
		},
		{
			title: 'Gesture-Based Motif Research',
			type: 'Research assistantship',
			status: '2024',
			copy:
				'A music technology research project using machine learning tools in Max to train and generate variations of musical motifs from user gestures.',
			tags: ['Max', 'machine learning', 'music', 'interaction']
		}
	];
</script>

<div class="page-shell">
	<section class="hero-panel hero-grid">
		<div>
			<h2>Projects</h2>
			<h1>Research that becomes usable systems.</h1>
			<p class="lead">
				Explore projects that transform complex cultural and musical questions into
				readable evidence, usable interfaces, and research people can act on.
			</p>
			<div class="button-row">
				<a class="button" href="#project-list">View Featured Work</a>
				<a class="button secondary" href="/contact">Collaborate</a>
			</div>
		</div>
	</section>

	<section class="project-list" id="project-list">
		{#each projects as project}
			<article class:featured={project.featured} class="project">
				<div>
					<p class="project-type">{project.type}</p>
					<h2>{project.title}</h2>
					<p>{project.copy}</p>
					<div class="meta">
						<span class="pill">{project.status}</span>
						{#each project.tags as tag}
							<span class="pill">{tag}</span>
						{/each}
					</div>
				</div>
				{#if project.href}
					<a class="button secondary" href={project.href} target="_blank" rel="noreferrer">GitHub</a>
				{/if}
			</article>
		{/each}
	</section>

	<section>
		<div class="section-head">
			<div>
				<h2>Music</h2>
				<h2>Original SoundCloud work</h2>
			</div>
			<p>Music remains part of my technical and research practice.</p>
		</div>

		<div class="player-shell">
			<iframe
				width="100%"
				height="300"
				allow="autoplay"
				src={embedUrl}
				title="SoundCloud player"
			></iframe>
		</div>
	</section>
</div>

<style>
	.project-list {
		display: grid;
		gap: clamp(34px, 6vw, 72px);
	}

	.project {
		display: grid;
		grid-template-columns: minmax(0, 1fr) auto;
		gap: clamp(24px, 5vw, 60px);
		align-items: start;
		border: 0;
		border-top: 1px solid #000000;
		border-radius: 0;
		padding: clamp(42px, 7vw, 86px) 0;
		background: transparent;
		box-shadow: none;
		transition:
			transform 220ms ease,
			background 220ms ease,
			border-color 220ms ease;
	}

	.project:hover {
		transform: translateY(-3px);
		border-color: #000000;
		background: transparent;
	}

	.project.featured {
		background: transparent;
	}

	.project p {
		max-width: 820px;
		margin: 24px 0 0;
	}

	.project h2 {
		max-width: 900px;
		font-size: clamp(2.25rem, 5vw, 4.8rem);
	}

	.project-type {
		margin: 0 0 18px !important;
		font-size: 0.88rem;
		font-weight: 850;
		letter-spacing: 0.12em;
		text-transform: uppercase;
	}

	.player-shell {
		overflow: hidden;
		border: 0;
		border-top: 1px solid #000000;
		border-radius: 0;
		background: transparent;
		box-shadow: none;
		padding-top: 18px;
	}

	iframe {
		display: block;
		border: 0;
	}

	@media (max-width: 760px) {
		.project {
			grid-template-columns: 1fr;
		}
	}
</style>
