<script lang="ts">
	import { onMount } from 'svelte';

	// What We Do / Who We Serve animations
	let whatWeDoVisible = $state(false);
	let whoWeServeVisible = $state(false);
	let marketTypesVisible = $state(false);
	let commercialProfilesVisible = $state(false);
	let goodFitVisible = $state(false);

	// Where Our Advisory Excels animations
	let excelsHeaderVisible = $state(false);
	let excelsCardsVisible = $state<boolean[]>([false, false, false, false]);

	// Problems We Solve animations
	let sectionVisible = $state(false);
	let itemsVisible = $state<boolean[]>(Array(9).fill(false));

	let isMobile = $state(false);

	onMount(() => {
		isMobile = window.matchMedia('(max-width: 768px)').matches;

		// What We Do / Who We Serve observer
		const whatWeDoObserver = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						if (isMobile) {
							// Immediate on mobile
							whatWeDoVisible = true;
							whoWeServeVisible = true;
							marketTypesVisible = true;
							commercialProfilesVisible = true;
							goodFitVisible = true;
						} else {
							setTimeout(() => whatWeDoVisible = true, 100);
							setTimeout(() => whoWeServeVisible = true, 300);
							setTimeout(() => marketTypesVisible = true, 500);
							setTimeout(() => commercialProfilesVisible = true, 700);
							setTimeout(() => goodFitVisible = true, 900);
						}
					}
				});
			},
			{ threshold: isMobile ? 0.05 : 0.2 }
		);

		const whatWeDoSection = document.getElementById('what-we-do');
		if (whatWeDoSection) whatWeDoObserver.observe(whatWeDoSection);

		// Where Our Advisory Excels observer
		const excelsObserver = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						excelsHeaderVisible = true;
						if (isMobile) {
							excelsCardsVisible = [true, true, true, true];
						} else {
							excelsCardsVisible.forEach((_, index) => {
								setTimeout(() => {
									excelsCardsVisible[index] = true;
								}, index * 150);
							});
						}
					}
				});
			},
			{ threshold: isMobile ? 0.05 : 0.2 }
		);

		const excelsSection = document.getElementById('excels-section');
		if (excelsSection) excelsObserver.observe(excelsSection);

		// Problems We Solve observer
		const problemsObserver = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						sectionVisible = true;
						if (isMobile) {
							itemsVisible = Array(9).fill(true);
						} else {
							itemsVisible.forEach((_, index) => {
								setTimeout(() => {
									itemsVisible[index] = true;
								}, index * 100);
							});
						}
					}
				});
			},
			{ threshold: isMobile ? 0.05 : 0.2 }
		);

		const section = document.getElementById('problems-section');
		if (section) problemsObserver.observe(section);

		return () => {
			whatWeDoObserver.disconnect();
			excelsObserver.disconnect();
			problemsObserver.disconnect();
		};
	});
	
	const problems = [
		'Inconsistent pipeline',
		'Referral dependency',
		'No dedicated demand channel',
		'Hard-to-reach buyers',
		'Brand-sensitive markets',
		'Long, complex sales cycles',
		'Customer concentration risk',
		'Underperforming outbound teams',
		'No forecasting visibility'
	];
	
	const excelsItems = [
		{
			title: 'Hard-to-reach buyers',
			description: 'Decision-makers who don\'t respond to traditional outreach'
		},
		{
			title: 'Brand-sensitive markets',
			description: 'Industries where reputation and trust are paramount'
		},
		{
			title: 'Complex, multi-stakeholder sales',
			description: 'Long cycles requiring careful navigation'
		},
		{
			title: 'Data-scarce environments',
			description: 'Markets lacking reliable contact data or intelligence'
		}
	];
</script>

<!-- What We Do / Who We Serve Section -->
<section id="what-we-do" class="py-12 md:py-20 border-b-2 border-navy">
	<div class="container-custom">
		<div class="grid grid-cols-1 lg:grid-cols-2 gap-10 md:gap-20">
			<!-- What We Do -->
			<div class={[
				'border-l-2 md:border-l-4 border-gold pl-4 md:pl-8 transition-all duration-500 md:duration-1000',
				whatWeDoVisible ? 'opacity-100 translate-x-0' : 'opacity-0 -translate-x-12'
			]}>
				<h2 class="text-2xl sm:text-3xl md:text-4xl font-serif font-bold mb-4 md:mb-6 text-navy">What We Do</h2>
				<p class="text-sm sm:text-base md:text-lg text-foreground leading-relaxed mb-4 md:mb-6 font-sans">
					We specialize in markets where buyers are sophisticated, brand reputation is high, and growth is on the horizon.
				</p>
				<p class="text-sm sm:text-base md:text-lg text-foreground leading-relaxed mb-4 md:mb-6 font-sans">
					Our approach combines deep market intelligence with enterprise-grade execution, designed specifically for industries where trust, precision, and reputation are non-negotiable. We work with leadership teams who understand that sustainable growth requires more than volume—it demands quality, strategic alignment, and a methodology built for careful, considered buyers.
				</p>
				<p class="text-sm sm:text-base md:text-lg text-foreground leading-relaxed mb-4 md:mb-6 font-sans hidden md:block">
					From institutional finance to legacy, strong markets in enterprise technology, we serve sectors where traditional demand generation fails. Our advisory-led model ensures every engagement is structured around your specific commercial reality, with clear benchmarks, conservative forecasting, and complete transparency at every stage.
				</p>
				<p class="text-sm sm:text-base md:text-lg text-foreground leading-relaxed mb-4 md:mb-6 font-sans hidden md:block">
					We don't replace your referral network or warm relationships. Instead, we build parallel, predictable channels that complement and scale what's already working, giving you control over pipeline without compromising the brand equity you've spent years building.
				</p>
			</div>

			<!-- Who We Serve -->
			<div id="who-we-serve" class={[
				'border-l-2 md:border-l-4 border-gold pl-4 md:pl-8 transition-all duration-500 md:duration-1000',
				whoWeServeVisible ? 'opacity-100 translate-x-0' : 'opacity-0 translate-x-12'
			]}>
				<h2 class="text-2xl sm:text-3xl md:text-4xl font-serif font-bold mb-4 md:mb-6 text-navy">Who We Serve</h2>
				<div class="space-y-4 md:space-y-6">
					<div class={[
						'transition-all duration-500 md:duration-700',
						marketTypesVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'
					]}>
						<h3 class="font-serif font-bold mb-2 md:mb-3 text-navy text-base md:text-xl">Market Types</h3>
						<ul class="text-muted space-y-1.5 md:space-y-2 text-sm md:text-base leading-relaxed font-sans">
							<li class="flex items-start gap-2"><span class="text-gold">•</span> Legacy & complex markets</li>
							<li class="flex items-start gap-2"><span class="text-gold">•</span> Fast-growth teams outpacing demand</li>
							<li class="flex items-start gap-2"><span class="text-gold">•</span> Referral-dependent businesses</li>
							<li class="flex items-start gap-2"><span class="text-gold">•</span> Companies with customer concentration risk</li>
						</ul>
					</div>
					<div class={[
						'transition-all duration-500 md:duration-700',
						commercialProfilesVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'
					]}>
						<h3 class="font-serif font-bold mb-2 md:mb-3 text-navy text-base md:text-xl">Commercial Profiles</h3>
						<ul class="text-muted space-y-1.5 md:space-y-2 text-sm md:text-base leading-relaxed font-sans">
							<li class="flex items-start gap-2"><span class="text-gold">•</span> High ACV / long sales cycles</li>
							<li class="flex items-start gap-2"><span class="text-gold">•</span> Low ACV / brand-sensitive volume</li>
							<li class="flex items-start gap-2"><span class="text-gold">•</span> Existing outbound teams</li>
							<li class="flex items-start gap-2"><span class="text-gold">•</span> No outbound at all</li>
						</ul>
					</div>
					<div class={[
						'transition-all duration-500 md:duration-700',
						goodFitVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'
					]}>
						<h3 class="font-serif font-bold mb-2 md:mb-3 text-navy text-base md:text-xl">Good-Fit Clients</h3>
						<ul class="text-muted space-y-1.5 md:space-y-2 text-sm md:text-base leading-relaxed font-sans">
							<li class="flex items-start gap-2"><span class="text-gold">•</span> Clear sales KPIs and close rates</li>
							<li class="flex items-start gap-2"><span class="text-gold">•</span> Leadership alignment (Finance, Sales, Ops)</li>
							<li class="flex items-start gap-2"><span class="text-gold">•</span> Non-commodity offerings</li>
						</ul>
					</div>
				</div>
			</div>
		</div>
	</div>
</section>

<!-- Where Our Advisory Excels -->
<section id="excels-section" class="py-12 md:py-20 border-b-2 border-navy bg-cream">
	<div class="container-custom">
		<div class={[
			'text-center mb-8 md:mb-12 transition-all duration-500 md:duration-1000',
			excelsHeaderVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'
		]}>
			<div class={[
				'w-16 md:w-24 h-0.5 bg-gold mx-auto mb-4 md:mb-6 transition-all duration-500 md:duration-700',
				excelsHeaderVisible ? 'scale-x-100' : 'scale-x-0'
			]}></div>
			<h2 class="text-2xl sm:text-3xl md:text-4xl font-serif font-bold mb-3 md:mb-4 text-navy px-2">Where Our Advisory Excels</h2>
			<div class={[
				'w-16 md:w-24 h-0.5 bg-gold mx-auto mt-4 md:mt-6 transition-all duration-500 md:duration-700',
				excelsHeaderVisible ? 'scale-x-100' : 'scale-x-0'
			]}></div>
		</div>

		<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4 md:gap-6">
			{#each excelsItems as item, index}
				<div class={[
					'group relative bg-background border-2 border-navy p-5 md:p-8 space-y-2 md:space-y-3 transition-all duration-500 md:duration-700',
					'md:hover:border-gold md:hover:scale-105 md:hover:-translate-y-2',
					excelsCardsVisible[index] ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'
				]} style={`transition-delay: ${isMobile ? 0 : index * 100}ms`}>
					<h3 class="font-serif font-bold text-base md:text-xl text-navy transition-all duration-300 md:group-hover:text-gold">{item.title}</h3>
					<p class="text-sm md:text-base text-muted leading-relaxed font-sans">{item.description}</p>

					<!-- Hover glow effect - desktop only -->
					<div class="hidden md:block absolute inset-0 bg-gold opacity-0 group-hover:opacity-5 transition-opacity duration-300 pointer-events-none"></div>
				</div>
			{/each}
		</div>
	</div>
</section>

<!-- Problems We Solve -->

<section id="problems-section" class="py-12 md:py-20 border-b-2 border-navy overflow-hidden">
	<div class="container-custom">
		<div class={[
			'text-center mb-8 md:mb-16 transition-all duration-500 md:duration-1000',
			sectionVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'
		]}>
			<div class={[
				'w-16 md:w-24 h-0.5 bg-gold mx-auto mb-4 md:mb-6 transition-all duration-500 md:duration-700',
				sectionVisible ? 'scale-x-100' : 'scale-x-0'
			]}></div>
			<h2 class="text-2xl sm:text-3xl md:text-4xl font-serif font-bold mb-3 md:mb-4 text-navy px-2">Problems We Solve</h2>
			<div class={[
				'w-16 md:w-24 h-0.5 bg-gold mx-auto mt-4 md:mt-6 transition-all duration-500 md:duration-700',
				sectionVisible ? 'scale-x-100' : 'scale-x-0'
			]}></div>
		</div>

		<!-- Animated grid with staggered entrance -->
		<div class="max-w-6xl mx-auto">
			<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 md:gap-6">
				{#each problems as problem, index}
					<div
						class={[
							'group relative bg-background border-2 border-gold p-4 md:p-6 transition-all duration-300 md:duration-500 cursor-pointer',
							'md:hover:border-navy md:hover:scale-105 md:hover:-translate-y-1',
							itemsVisible[index] ? 'opacity-100 translate-y-0 rotate-0' : 'opacity-0 translate-y-12 -rotate-3'
						]}
						style={`transition-delay: ${isMobile ? 0 : index * 50}ms`}
					>
						<!-- Animated border accent - desktop only -->
						<div class="hidden md:block absolute top-0 left-0 w-0 h-0.5 bg-navy transition-all duration-500 group-hover:w-full"></div>
						<div class="hidden md:block absolute bottom-0 right-0 w-0 h-0.5 bg-navy transition-all duration-500 group-hover:w-full"></div>
						<div class="hidden md:block absolute top-0 left-0 w-0.5 h-0 bg-navy transition-all duration-500 group-hover:h-full"></div>
						<div class="hidden md:block absolute top-0 right-0 w-0.5 h-0 bg-navy transition-all duration-500 group-hover:h-full"></div>

						<!-- Number indicator -->
						<div class={[
							'absolute -top-2.5 -left-2.5 md:-top-3 md:-left-3 w-6 h-6 md:w-8 md:h-8 rounded-full bg-gold flex items-center justify-center',
							'font-sans font-bold text-xs md:text-sm text-navy transition-all duration-300',
							'md:group-hover:scale-125 md:group-hover:bg-navy md:group-hover:text-gold'
						]}>
							{index + 1}
						</div>

						<!-- Content -->
						<div class="relative z-10 ml-2 md:ml-0">
							<p class={[
								'text-sm md:text-lg font-sans font-semibold text-navy transition-all duration-300',
								'md:group-hover:text-navy md:group-hover:translate-x-1'
							]}>
								{problem}
							</p>
						</div>

						<!-- Hover glow effect - desktop only -->
						<div class="hidden md:block absolute inset-0 bg-gold opacity-0 group-hover:opacity-5 transition-opacity duration-300 pointer-events-none"></div>
					</div>
				{/each}
			</div>
		</div>

		<!-- Animated decorative elements - hidden on mobile for performance -->
		<div class="hidden md:block relative mt-16 h-32 overflow-hidden">
			<div class={[
				'absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2',
				'w-64 h-64 border border-gold rounded-full transition-all duration-[2000ms]',
				sectionVisible ? 'opacity-20 scale-100' : 'opacity-0 scale-0'
			]}></div>
			<div class={[
				'absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2',
				'w-48 h-48 border border-navy rounded-full transition-all duration-[2000ms] delay-300',
				sectionVisible ? 'opacity-20 scale-100' : 'opacity-0 scale-0'
			]}></div>
			<div class={[
				'absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2',
				'w-32 h-32 bg-gold rounded-full transition-all duration-[2000ms] delay-500',
				sectionVisible ? 'opacity-10 scale-100' : 'opacity-0 scale-0'
			]}></div>
		</div>
	</div>
</section>
