<script lang="ts">
	import { onMount } from 'svelte';

	let headerVisible = $state(false);
	let cardsVisible = $state<boolean[]>(Array(9).fill(false));
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
							cardsVisible = Array(9).fill(true);
						} else {
							// Stagger card animations on desktop
							cardsVisible.forEach((_, index) => {
								setTimeout(() => {
									cardsVisible[index] = true;
								}, index * 80);
							});
						}
					}
				});
			},
			{ threshold: isMobile ? 0.05 : 0.1 }
		);

		const section = document.getElementById('how-we-work');
		if (section) observer.observe(section);

		return () => observer.disconnect();
	});

	const steps = [
		{
			number: '01',
			title: 'Selective Engagement & Fit',
			description: 'We work with a limited number of clients. Engagement begins only with executive intent and alignment.'
		},
		{
			number: '02',
			title: 'Full-Funnel Commercial Diligence',
			description: 'We assess the entire revenue system: demand → qualification → sales → close. This is where vendors fail. We don\'t.'
		},
		{
			number: '03',
			title: 'Scope & Risk-Managed Structure',
			description: '2–6 weeks to validate assumptions, define qualified demand, and structure outcome-tied engagements with defensible ROI.'
		},
		{
			number: '04',
			title: 'Rigorous Onboarding',
			description: 'Leadership interviews, analyst research, buyer mapping, message architecture, and brand guardrails.'
		},
		{
			number: '05',
			title: 'Channel-Agnostic Execution',
			description: 'We deploy demand systems based on where buyers actually are — using enterprise-safe, reputation-first infrastructure.'
		},
		{
			number: '06',
			title: 'Multi-Disciplinary Team',
			description: 'Advisors, former founders, sales leaders, analysts, operators, and trusted vendors (75+ years combined experience).'
		},
		{
			number: '07',
			title: 'Pipeline Delivery & Validation',
			description: 'Qualified conversations benchmarked to your ACV, LTV, and sales cycle. Leadership-level visibility throughout.'
		},
		{
			number: '08',
			title: 'ROI-Driven Engagements',
			description: 'Clear milestones, conservative modeling, downside protection.'
		},
		{
			number: '09',
			title: 'Ongoing Advisory & Optimization',
			description: 'Continuous refinement of data, messaging, execution, and reporting. Systems compound over time.'
		}
	];
</script>

<section id="how-we-work" class="py-12 md:py-24 border-b-2 border-navy bg-cream">
	<div class="container-custom">
		<!-- Decorative header -->
		<div class={[
			'mb-8 md:mb-16 text-center transition-all duration-500 md:duration-1000',
			headerVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'
		]}>
			<div class={[
				'w-16 md:w-24 h-0.5 bg-gold mx-auto mb-4 md:mb-6 transition-all duration-500 md:duration-700',
				headerVisible ? 'scale-x-100' : 'scale-x-0'
			]}></div>
			<h2 class="text-2xl sm:text-3xl md:text-5xl font-serif font-bold mb-3 md:mb-4 text-navy px-2">How We Work</h2>
			<p class="text-base md:text-xl text-foreground max-w-2xl mx-auto leading-relaxed font-sans px-4">
				Structured, advisory-grade process for sophisticated buyers
			</p>
			<div class={[
				'w-16 md:w-24 h-0.5 bg-gold mx-auto mt-4 md:mt-6 transition-all duration-500 md:duration-700',
				headerVisible ? 'scale-x-100' : 'scale-x-0'
			]}></div>
		</div>

		<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 md:gap-6">
			{#each steps as step, index}
				<div class={[
					'group relative border-2 border-navy bg-background p-5 md:p-8 space-y-3 md:space-y-4 transition-all duration-500 md:duration-700',
					'md:hover:border-gold md:hover:scale-105 md:hover:-translate-y-2',
					cardsVisible[index] ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'
				]} style={`transition-delay: ${isMobile ? 0 : index * 50}ms`}>
					<div class="flex items-center gap-2 md:gap-3 mb-2 md:mb-3">
						<span class="font-sans text-xs md:text-sm text-gold font-bold transition-all duration-300 md:group-hover:scale-125">{step.number}</span>
						<div class="h-0.5 bg-gold flex-1 transition-all duration-500 origin-left md:group-hover:scale-x-110"></div>
					</div>
					<h3 class="font-serif font-bold text-base md:text-xl text-navy transition-all duration-300 md:group-hover:text-gold">{step.title}</h3>
					<p class="text-sm md:text-base text-muted leading-relaxed font-sans">
						{step.description}
					</p>

					<!-- Hover glow effect - desktop only -->
					<div class="hidden md:block absolute inset-0 bg-gold opacity-0 group-hover:opacity-5 transition-opacity duration-300 pointer-events-none"></div>
				</div>
			{/each}
		</div>
	</div>
</section>
