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

<section class="py-24 border-b-2 border-navy overflow-hidden bg-cream">
	<div class="container-custom">
		<div class="text-center mb-16">
			<div class="w-24 h-0.5 bg-gold mx-auto mb-6"></div>
			<h2 class="text-3xl font-display font-semibold mb-4 text-navy">Industries We Serve</h2>
			<p class="text-base text-foreground max-w-2xl mx-auto leading-relaxed">
				Specialized expertise across brand-sensitive and complex markets
			</p>
			<div class="w-24 h-0.5 bg-gold mx-auto mt-6"></div>
		</div>
		
		<!-- Sliding Industries Container -->
		<div class="relative">
			<!-- Gradient overlays for fade effect -->
			<div class="absolute left-0 top-0 bottom-0 w-32 bg-gradient-to-r from-cream to-transparent z-10 pointer-events-none"></div>
			<div class="absolute right-0 top-0 bottom-0 w-32 bg-gradient-to-l from-cream to-transparent z-10 pointer-events-none"></div>
			
			<!-- Scrolling content -->
			<div class="industries-track">
				<div class="industries-content">
					{#each industries as industry}
						<div class="industry-item">
							<span class="text-sm font-display font-semibold text-navy">{industry}</span>
						</div>
					{/each}
					<!-- Duplicate for seamless loop -->
					{#each industries as industry}
						<div class="industry-item">
							<span class="text-sm font-display font-semibold text-navy">{industry}</span>
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
		gap: 2rem;
		animation: scroll 40s linear infinite;
		will-change: transform;
	}
	
	.industry-item {
		flex-shrink: 0;
		padding: 1.25rem 2.5rem;
		border: 2px solid var(--color-navy);
		background: var(--color-background);
		white-space: nowrap;
		transition: transform 0.3s ease, border-color 0.3s ease, background-color 0.3s ease;
	}
	
	.industry-item:hover {
		transform: translateY(-3px);
		border-color: var(--color-gold);
		background: var(--color-cream);
	}
	
	@keyframes scroll {
		0% {
			transform: translateX(0);
		}
		100% {
			transform: translateX(-50%);
		}
	}
	
	/* Pause animation on hover */
	.industries-track:hover .industries-content {
		animation-play-state: paused;
	}
	
	/* Responsive adjustments */
	@media (max-width: 768px) {
		.industries-content {
			animation-duration: 30s;
		}
		
		.industry-item {
			padding: 0.75rem 1.5rem;
		}
	}
</style>
