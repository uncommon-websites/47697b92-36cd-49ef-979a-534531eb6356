<script lang="ts">
	import { onMount } from 'svelte';

	let headerVisible = $state(false);
	let cardsVisible = $state<boolean[]>([false, false, false, false]);
	let isMobile = $state(false);

	onMount(() => {
		isMobile = window.matchMedia('(max-width: 768px)').matches;

		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						headerVisible = true;
						if (isMobile) {
							// Show all immediately on mobile
							cardsVisible = [true, true, true, true];
						} else {
							cardsVisible.forEach((_, index) => {
								setTimeout(() => {
									cardsVisible[index] = true;
								}, index * 150);
							});
						}
					}
				});
			},
			{ threshold: isMobile ? 0.1 : 0.2 }
		);

		const section = document.getElementById('why-us');
		if (section) observer.observe(section);

		return () => observer.disconnect();
	});

	const features = [
		{
			icon: 'M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z',
			title: 'Built for careful buyers',
			description: 'Private, enterprise-safe infrastructure designed for markets where reputation is everything.'
		},
		{
			icon: 'M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-3 7h3m-3 4h3m-6-4h.01M9 16h.01',
			title: 'Analyst-led market intelligence',
			description: 'Deep research and buyer mapping that informs every touchpoint and message.'
		},
		{
			icon: 'M5 3v4M3 5h4M6 17v4m-2-2h4m5-16l2.286 6.857L21 12l-5.714 2.143L13 21l-2.286-6.857L5 12l5.714-2.143L13 3z',
			title: 'Brand integrity preserved',
			description: 'Every campaign is designed with your reputation in mind, never compromising trust for volume.'
		},
		{
			icon: 'M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z',
			title: 'Predictable conversion benchmarks',
			description: 'Clear milestones, conservative modeling, and downside protection with leadership-level visibility.'
		}
	];
</script>

<section id="why-us" class="py-12 md:py-20 border-b-2 border-navy">
	<div class="container-custom">
		<div class={[
			'text-center mb-10 md:mb-16 transition-all duration-500 md:duration-1000',
			headerVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'
		]}>
			<div class={[
				'w-16 md:w-24 h-0.5 bg-gold mx-auto mb-4 md:mb-6 transition-all duration-500 md:duration-700',
				headerVisible ? 'scale-x-100' : 'scale-x-0'
			]}></div>
			<h2 class="text-2xl sm:text-3xl md:text-5xl font-display font-bold mb-3 md:mb-4 text-navy px-2">Why Leading Companies Choose Us</h2>
			<p class="text-foreground text-sm sm:text-base md:text-lg max-w-2xl mx-auto leading-relaxed font-medium px-4">
				We combine deep market expertise with enterprise-grade execution to deliver results that matter.
			</p>
			<div class={[
				'w-16 md:w-24 h-0.5 bg-gold mx-auto mt-4 md:mt-6 transition-all duration-500 md:duration-700',
				headerVisible ? 'scale-x-100' : 'scale-x-0'
			]}></div>
		</div>

		<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6 md:gap-8">
			{#each features as feature, index}
				<div class={[
					'group space-y-3 md:space-y-4 border-l-2 border-gold pl-4 md:pl-6 transition-all duration-500 md:duration-700',
					'md:hover:translate-x-2',
					cardsVisible[index] ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'
				]} style={`transition-delay: ${isMobile ? 0 : index * 100}ms`}>
					<div class="w-10 h-10 md:w-12 md:h-12 border-2 border-navy flex items-center justify-center bg-cream transition-all duration-300 md:group-hover:border-gold md:group-hover:scale-110">
						<svg class="w-5 h-5 md:w-6 md:h-6 text-navy transition-colors duration-300 md:group-hover:text-gold" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d={feature.icon}></path>
						</svg>
					</div>
					<h3 class="font-display font-bold text-base md:text-lg text-navy transition-colors duration-300 md:group-hover:text-gold">{feature.title}</h3>
					<p class="text-sm md:text-base text-muted leading-relaxed font-medium">
						{feature.description}
					</p>
				</div>
			{/each}
		</div>
	</div>
</section>
