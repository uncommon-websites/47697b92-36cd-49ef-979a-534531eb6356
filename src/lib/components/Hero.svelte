<script lang="ts">
	import { onMount } from 'svelte';
	
	let heroVisible = $state(false);
	let decorativeLineVisible = $state(false);
	let headingVisible = $state(false);
	let subheadingVisible = $state(false);
	let taglineVisible = $state(false);
	let bulletsVisible = $state<boolean[]>([false, false, false]);
	let ctasVisible = $state(false);
	let imageVisible = $state(false);
	let overlayVisible = $state(false);
	
	onMount(() => {
		// Staggered entrance animation
		setTimeout(() => decorativeLineVisible = true, 100);
		setTimeout(() => headingVisible = true, 300);
		setTimeout(() => subheadingVisible = true, 600);
		setTimeout(() => taglineVisible = true, 900);
		setTimeout(() => bulletsVisible[0] = true, 1200);
		setTimeout(() => bulletsVisible[1] = true, 1350);
		setTimeout(() => bulletsVisible[2] = true, 1500);
		setTimeout(() => ctasVisible = true, 1700);
		setTimeout(() => imageVisible = true, 1900);
		setTimeout(() => overlayVisible = true, 2200);
	});
</script>

<section class="pt-24 pb-20 overflow-hidden border-b-2 border-navy">
	<div class="container-custom">
		<!-- Decorative top line -->
		<div class={[
			'w-24 h-0.5 bg-gold mb-8 transition-all duration-700',
			decorativeLineVisible ? 'opacity-100 scale-x-100' : 'opacity-0 scale-x-0'
		]}></div>
		
		<div class="max-w-4xl mb-12">
			<h1 class={[
				'text-5xl md:text-6xl lg:text-7xl font-bold mb-8 text-navy transition-all duration-1000',
				headingVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'
			]} style="letter-spacing: -0.025em; line-height: 1.1; font-weight: 700;">
				Qualified Demand for Companies With Sophisticated Buyers
			</h1>
			<p class={[
				'text-xl md:text-2xl text-foreground mb-6 leading-relaxed transition-all duration-1000',
				subheadingVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'
			]}>
				We help operators in complex industries build predictable, high-quality pipeline — without referrals, guesswork, or risky lead gen.
			</p>
			<p class={[
				'text-base text-muted mb-10 max-w-2xl border-l-2 border-gold pl-4 transition-all duration-1000',
				taglineVisible ? 'opacity-100 translate-x-0' : 'opacity-0 -translate-x-8'
			]}>
				Specialists in markets where buyers are careful, stakes are high, and message precision matters.
			</p>

			<!-- Supporting Bullets -->
			<div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-12 max-w-3xl">
				<div class={[
					'flex items-start gap-3 border-l-2 border-accent pl-4 transition-all duration-700',
					bulletsVisible[0] ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'
				]}>
					<span class="text-gold text-lg">•</span>
					<span class="text-sm leading-relaxed">Predictable access to hard-to-reach markets</span>
				</div>
				<div class={[
					'flex items-start gap-3 border-l-2 border-accent pl-4 transition-all duration-700',
					bulletsVisible[1] ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'
				]}>
					<span class="text-gold text-lg">•</span>
					<span class="text-sm leading-relaxed">Built for brand-sensitive industries</span>
				</div>
				<div class={[
					'flex items-start gap-3 border-l-2 border-accent pl-4 transition-all duration-700',
					bulletsVisible[2] ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'
				]}>
					<span class="text-gold text-lg">•</span>
					<span class="text-sm leading-relaxed">Advisory-led strategy, not a vendor model</span>
				</div>
			</div>

			<!-- CTAs -->
			<div class={[
				'flex flex-wrap gap-4 transition-all duration-1000',
				ctasVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'
			]}>
				<a href="#contact" class="bg-navy text-cream px-8 py-4 text-sm font-mono uppercase hover:bg-forest transition-all duration-300 flex items-center gap-2 border border-navy hover:border-gold hover:scale-105">
					Book a Discovery Call
					<svg width="12" height="12" viewBox="0 0 12 12" fill="none" xmlns="http://www.w3.org/2000/svg">
						<path d="M1 11L11 1M11 1H3M11 1V9" stroke="currentColor" stroke-width="1.5"/>
					</svg>
				</a>
				<a href="#results" class="border-2 border-navy px-8 py-4 text-sm font-mono uppercase hover:bg-cream transition-all duration-300 text-navy hover:scale-105">
					See Recent Wins
				</a>
			</div>
		</div>

		<div class={[
			'relative w-full aspect-[21/9] overflow-hidden border-4 border-navy transition-all duration-1000',
			imageVisible ? 'opacity-100 scale-100' : 'opacity-0 scale-95'
		]}>
			<!-- Hero Image -->
			<img 
				src="/generated/image-diverse-group-of-business-professionals--1765567878019-2.webp" 
				alt="Modern work environment with business professionals" 
				class="absolute inset-0 w-full h-full object-cover"
			/>
			
			<!-- Subtle overlay for depth -->
			<div class="absolute inset-0 bg-gradient-to-t from-navy/70 via-navy/20 to-transparent"></div>
			
			<!-- Content overlay with classic styling -->
			<div class="absolute inset-0 flex items-end justify-start p-10">
				<div class={[
					'inline-block border-2 border-gold bg-navy/80 backdrop-blur-sm px-8 py-4 text-cream text-sm font-mono uppercase tracking-wider transition-all duration-1000',
					overlayVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'
				]}>
					Advisory-Grade Demand Generation
				</div>
			</div>
		</div>
	</div>
</section>
