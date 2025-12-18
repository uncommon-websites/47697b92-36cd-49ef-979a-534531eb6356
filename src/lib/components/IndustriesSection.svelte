<script lang="ts">
	// Industries data
	const industries = [
		'Institutional Finance',
		'Private Equity',
		'Family Offices',
		'Enterprise Tech',
		'Industrials',
		'Professional Services',
		'Healthcare',
		'Gov/Defense-Adjacent'
	];
</script>

<section class="py-12 md:py-24 border-b-2 border-navy overflow-hidden bg-cream">
	<div class="container-custom">
		<div class="text-center mb-8 md:mb-16">
			<div class="w-16 md:w-24 h-0.5 bg-gold mx-auto mb-4 md:mb-6"></div>
			<h2 class="text-2xl sm:text-3xl md:text-4xl font-serif font-bold mb-3 md:mb-4 text-navy px-2">Industries We Serve</h2>
			<p class="text-sm sm:text-base md:text-lg text-foreground max-w-2xl mx-auto leading-relaxed font-sans px-4">
				Specialized expertise across brand-sensitive and complex markets
			</p>
			<div class="w-16 md:w-24 h-0.5 bg-gold mx-auto mt-4 md:mt-6"></div>
		</div>

		<!-- Sliding Industries Container -->
		<div class="relative">
			<!-- Gradient overlays for fade effect -->
			<div class="absolute left-0 top-0 bottom-0 w-8 md:w-32 bg-gradient-to-r from-cream to-transparent z-10 pointer-events-none"></div>
			<div class="absolute right-0 top-0 bottom-0 w-8 md:w-32 bg-gradient-to-l from-cream to-transparent z-10 pointer-events-none"></div>

			<!-- Scrolling content -->
			<div class="industries-track">
				<div class="industries-content">
					{#each industries as industry}
						<div class="industry-item">
							<span class="text-xs sm:text-sm md:text-base font-sans font-semibold text-navy">{industry}</span>
						</div>
					{/each}
					<!-- Duplicate for seamless loop -->
					{#each industries as industry}
						<div class="industry-item">
							<span class="text-xs sm:text-sm md:text-base font-sans font-semibold text-navy">{industry}</span>
						</div>
					{/each}
				</div>
			</div>
		</div>
	</div>
</section>

<style>
	.industries-track {
		display: flex;
		overflow: hidden;
		position: relative;
	}

	.industries-content {
		display: flex;
		gap: 1rem;
		animation: scroll 35s linear infinite;
		will-change: transform;
	}

	.industry-item {
		flex-shrink: 0;
		padding: 0.625rem 1rem;
		border: 2px solid var(--color-navy);
		background: var(--color-background);
		white-space: nowrap;
		transition: border-color 0.3s ease, background-color 0.3s ease;
	}

	@keyframes scroll {
		0% {
			transform: translateX(0);
		}
		100% {
			transform: translateX(-50%);
		}
	}

	/* Desktop enhancements */
	@media (min-width: 768px) {
		.industries-content {
			gap: 2rem;
			animation-duration: 40s;
		}

		.industry-item {
			padding: 1.25rem 2.5rem;
			transition: transform 0.3s ease, border-color 0.3s ease, background-color 0.3s ease;
		}

		.industry-item:hover {
			transform: translateY(-3px);
			border-color: var(--color-gold);
			background: var(--color-cream);
		}

		/* Pause animation on hover - desktop only */
		.industries-track:hover .industries-content {
			animation-play-state: paused;
		}
	}

	/* Reduce motion for accessibility and mobile performance */
	@media (prefers-reduced-motion: reduce) {
		.industries-content {
			animation: none;
		}
	}
</style>
