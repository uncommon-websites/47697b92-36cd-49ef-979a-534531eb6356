<!-- What We Do / Who We Serve Section -->
<section id="what-we-do" class="py-20 border-b-2 border-navy">
	<div class="container-custom">
		<div class="grid grid-cols-1 lg:grid-cols-2 gap-20">
			<!-- What We Do -->
			<div class="border-l-4 border-gold pl-8">
				<h2 class="text-3xl font-display font-semibold mb-6 text-navy">What We Do</h2>
				<p class="text-base text-foreground leading-relaxed mb-6">
					We build predictable, high-quality demand channels for companies with sophisticated buyers — often outperforming referrals.
				</p>
			</div>

			<!-- Who We Serve -->
			<div id="who-we-serve" class="border-l-4 border-gold pl-8">
				<h2 class="text-3xl font-display font-semibold mb-6 text-navy">Who We Serve</h2>
				<div class="space-y-6 text-sm">
					<div>
						<h3 class="font-display font-semibold mb-3 text-navy text-base">Market Types</h3>
						<ul class="text-muted space-y-2 text-sm leading-relaxed">
							<li class="flex items-start gap-2"><span class="text-gold">•</span> Legacy & complex markets</li>
							<li class="flex items-start gap-2"><span class="text-gold">•</span> Fast-growth teams outpacing demand</li>
							<li class="flex items-start gap-2"><span class="text-gold">•</span> Referral-dependent businesses</li>
							<li class="flex items-start gap-2"><span class="text-gold">•</span> Companies with customer concentration risk</li>
						</ul>
					</div>
					<div>
						<h3 class="font-display font-semibold mb-3 text-navy text-base">Commercial Profiles</h3>
						<ul class="text-muted space-y-2 text-sm leading-relaxed">
							<li class="flex items-start gap-2"><span class="text-gold">•</span> High ACV / long sales cycles</li>
							<li class="flex items-start gap-2"><span class="text-gold">•</span> Low ACV / brand-sensitive volume</li>
							<li class="flex items-start gap-2"><span class="text-gold">•</span> Existing outbound teams</li>
							<li class="flex items-start gap-2"><span class="text-gold">•</span> No outbound at all</li>
						</ul>
					</div>
					<div>
						<h3 class="font-display font-semibold mb-3 text-navy text-base">Good-Fit Clients</h3>
						<ul class="text-muted space-y-2 text-sm leading-relaxed">
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
<section class="py-20 border-b-2 border-navy bg-cream">
	<div class="container-custom">
		<div class="text-center mb-12">
			<div class="w-24 h-0.5 bg-gold mx-auto mb-6"></div>
			<h2 class="text-3xl font-display font-semibold mb-4 text-navy">Where Our Advisory Excels</h2>
			<div class="w-24 h-0.5 bg-gold mx-auto mt-6"></div>
		</div>
		
		<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
			<div class="bg-background border-2 border-navy p-8 space-y-3 hover:border-gold transition-all duration-300">
				<h3 class="font-display font-semibold text-base text-navy">Hard-to-reach buyers</h3>
				<p class="text-sm text-muted leading-relaxed">Decision-makers who don't respond to traditional outreach</p>
			</div>
			
			<div class="bg-background border-2 border-navy p-8 space-y-3 hover:border-gold transition-all duration-300">
				<h3 class="font-display font-semibold text-base text-navy">Brand-sensitive markets</h3>
				<p class="text-sm text-muted leading-relaxed">Industries where reputation and trust are paramount</p>
			</div>
			
			<div class="bg-background border-2 border-navy p-8 space-y-3 hover:border-gold transition-all duration-300">
				<h3 class="font-display font-semibold text-base text-navy">Complex, multi-stakeholder sales</h3>
				<p class="text-sm text-muted leading-relaxed">Long cycles requiring careful navigation</p>
			</div>
			
			<div class="bg-background border-2 border-navy p-8 space-y-3 hover:border-gold transition-all duration-300">
				<h3 class="font-display font-semibold text-base text-navy">Data-scarce environments</h3>
				<p class="text-sm text-muted leading-relaxed">Markets lacking reliable contact data or intelligence</p>
			</div>
		</div>
	</div>
</section>

<!-- Problems We Solve -->
<script lang="ts">
	import { onMount } from 'svelte';
	
	let sectionVisible = $state(false);
	let itemsVisible = $state<boolean[]>(Array(9).fill(false));
	
	onMount(() => {
		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						sectionVisible = true;
						// Stagger the animation of each item
						itemsVisible.forEach((_, index) => {
							setTimeout(() => {
								itemsVisible[index] = true;
							}, index * 100);
						});
					}
				});
			},
			{ threshold: 0.2 }
		);
		
		const section = document.getElementById('problems-section');
		if (section) observer.observe(section);
		
		return () => observer.disconnect();
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
</script>

<section id="problems-section" class="py-20 border-b-2 border-navy overflow-hidden">
	<div class="container-custom">
		<div class={[
			'text-center mb-16 transition-all duration-1000',
			sectionVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'
		]}>
			<div class={[
				'w-24 h-0.5 bg-gold mx-auto mb-6 transition-all duration-700 delay-200',
				sectionVisible ? 'scale-x-100' : 'scale-x-0'
			]}></div>
			<h2 class="text-3xl font-display font-semibold mb-4 text-navy">Problems We Solve</h2>
			<div class={[
				'w-24 h-0.5 bg-gold mx-auto mt-6 transition-all duration-700 delay-200',
				sectionVisible ? 'scale-x-100' : 'scale-x-0'
			]}></div>
		</div>
		
		<!-- Animated grid with staggered entrance -->
		<div class="max-w-5xl mx-auto">
			<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
				{#each problems as problem, index}
					<div 
						class={[
							'group relative bg-background border-2 border-gold p-6 transition-all duration-500 cursor-pointer',
							'hover:border-navy hover:scale-105 hover:-translate-y-1',
							itemsVisible[index] ? 'opacity-100 translate-y-0 rotate-0' : 'opacity-0 translate-y-12 -rotate-3'
						]}
						style={`transition-delay: ${index * 50}ms`}
					>
						<!-- Animated border accent -->
						<div class="absolute top-0 left-0 w-0 h-0.5 bg-navy transition-all duration-500 group-hover:w-full"></div>
						<div class="absolute bottom-0 right-0 w-0 h-0.5 bg-navy transition-all duration-500 group-hover:w-full"></div>
						<div class="absolute top-0 left-0 w-0.5 h-0 bg-navy transition-all duration-500 group-hover:h-full"></div>
						<div class="absolute top-0 right-0 w-0.5 h-0 bg-navy transition-all duration-500 group-hover:h-full"></div>
						
						<!-- Number indicator -->
						<div class={[
							'absolute -top-3 -left-3 w-8 h-8 rounded-full bg-gold flex items-center justify-center',
							'font-display font-semibold text-sm text-navy transition-all duration-300',
							'group-hover:scale-125 group-hover:bg-navy group-hover:text-gold'
						]}>
							{index + 1}
						</div>
						
						<!-- Content -->
						<div class="relative z-10">
							<p class={[
								'text-base font-display text-navy transition-all duration-300',
								'group-hover:text-navy group-hover:translate-x-1'
							]}>
								{problem}
							</p>
						</div>
						
						<!-- Hover glow effect -->
						<div class="absolute inset-0 bg-gold opacity-0 group-hover:opacity-5 transition-opacity duration-300 pointer-events-none"></div>
					</div>
				{/each}
			</div>
		</div>
		
		<!-- Animated decorative elements -->
		<div class="relative mt-16 h-32 overflow-hidden">
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
