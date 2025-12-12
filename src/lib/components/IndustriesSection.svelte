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

<section class="py-20 border-b border-border overflow-hidden bg-gray-50">
	<div class="container-custom">
		<div class="text-center mb-12">
			<h2 class="text-2xl font-medium mb-3">Industries We Serve</h2>
			<p class="text-sm text-muted max-w-2xl mx-auto">
				Specialized expertise across brand-sensitive and complex markets
			</p>
		</div>
		
		<!-- Sliding Industries Container -->
		<div class="relative">
			<!-- Gradient overlays for fade effect -->
			<div class="absolute left-0 top-0 bottom-0 w-24 bg-gradient-to-r from-gray-50 to-transparent z-10 pointer-events-none"></div>
			<div class="absolute right-0 top-0 bottom-0 w-24 bg-gradient-to-l from-gray-50 to-transparent z-10 pointer-events-none"></div>
			
			<!-- Scrolling content -->
			<div class="industries-track">
				<div class="industries-content">
					{#each industries as industry}
						<div class="industry-item">
							<span class="text-sm font-medium text-foreground">{industry}</span>
						</div>
					{/each}
					<!-- Duplicate for seamless loop -->
					{#each industries as industry}
						<div class="industry-item">
							<span class="text-sm font-medium text-foreground">{industry}</span>
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
		padding: 1rem 2rem;
		border: 1px solid var(--border);
		background: white;
		white-space: nowrap;
		transition: transform 0.3s ease, border-color 0.3s ease;
	}
	
	.industry-item:hover {
		transform: translateY(-2px);
		border-color: var(--accent);
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
