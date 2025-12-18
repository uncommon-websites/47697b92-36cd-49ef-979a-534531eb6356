<script lang="ts">
	import { onMount } from 'svelte';

	let decorativeLineVisible = $state(false);
	let headingVisible = $state(false);
	let subheadingVisible = $state(false);
	let taglineVisible = $state(false);
	let bulletsVisible = $state<boolean[]>([false, false, false]);
	let ctasVisible = $state(false);
	let imageVisible = $state(false);
	let overlayVisible = $state(false);
	let isMobile = $state(false);

	onMount(() => {
		// Check if mobile for reduced animations
		isMobile = window.matchMedia('(max-width: 768px)').matches;

		if (isMobile) {
			// Faster, simpler animations on mobile
			decorativeLineVisible = true;
			headingVisible = true;
			subheadingVisible = true;
			taglineVisible = true;
			bulletsVisible = [true, true, true];
			ctasVisible = true;
			imageVisible = true;
			overlayVisible = true;
		} else {
			// Staggered entrance animation on desktop
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
		}
	});
</script>

<section class="pt-12 pb-12 md:pt-24 md:pb-20 overflow-hidden border-b-2 border-navy">
	<div class="container-custom">
		<!-- Decorative top line -->
		<div class={[
			'w-16 md:w-24 h-0.5 bg-gold mb-6 md:mb-8 transition-all duration-500 md:duration-700',
			decorativeLineVisible ? 'opacity-100 scale-x-100' : 'opacity-0 scale-x-0'
		]}></div>

		<div class="max-w-5xl mb-8 md:mb-12">
			<h1 class={[
				'text-2xl sm:text-3xl md:text-5xl lg:text-6xl font-serif font-bold mb-4 md:mb-8 text-navy transition-all duration-500 md:duration-1000',
				headingVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'
			]} style="letter-spacing: -0.02em; line-height: 1.2;">
				Qualified demand for companies with sophisticated buyers.
			</h1>
			<p class={[
				'text-base sm:text-lg md:text-2xl text-foreground mb-4 md:mb-6 leading-relaxed font-sans transition-all duration-500 md:duration-1000',
				subheadingVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'
			]}>
				Without replacing their referrals, warm network, and unpredictable growth channels.
			</p>
			<p class={[
				'text-sm sm:text-base md:text-lg text-muted mb-6 md:mb-10 max-w-2xl border-l-2 border-gold pl-3 md:pl-4 font-sans transition-all duration-500 md:duration-1000',
				taglineVisible ? 'opacity-100 translate-x-0' : 'opacity-0 -translate-x-8'
			]}>
				Specialists in markets where buyers are careful, stakes are high, and message precision matters.
			</p>

			<!-- Supporting Bullets -->
			<div class="grid grid-cols-1 gap-3 md:grid-cols-3 md:gap-6 mb-8 md:mb-12 max-w-3xl">
				<div class={[
					'flex items-start gap-2 md:gap-3 border-l-2 border-accent pl-3 md:pl-4 transition-all duration-500 md:duration-700',
					bulletsVisible[0] ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'
				]}>
					<span class="text-gold text-base md:text-lg">•</span>
					<span class="text-sm md:text-base leading-relaxed font-sans">Predictable access to hard-to-reach markets</span>
				</div>
				<div class={[
					'flex items-start gap-2 md:gap-3 border-l-2 border-accent pl-3 md:pl-4 transition-all duration-500 md:duration-700',
					bulletsVisible[1] ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'
				]}>
					<span class="text-gold text-base md:text-lg">•</span>
					<span class="text-sm md:text-base leading-relaxed font-sans">Built for brand-sensitive industries</span>
				</div>
				<div class={[
					'flex items-start gap-2 md:gap-3 border-l-2 border-accent pl-3 md:pl-4 transition-all duration-500 md:duration-700',
					bulletsVisible[2] ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'
				]}>
					<span class="text-gold text-base md:text-lg">•</span>
					<span class="text-sm md:text-base leading-relaxed font-sans">Advisory-led strategy, not a vendor model</span>
				</div>
			</div>

			<!-- CTAs -->
			<div class={[
				'flex flex-wrap gap-3 md:gap-4 transition-all duration-500 md:duration-1000',
				ctasVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'
			]}>
				<a href="#results" class="border-2 border-navy px-5 py-3 md:px-8 md:py-4 text-xs md:text-sm font-sans uppercase font-semibold tracking-wide hover:bg-cream transition-all duration-300 text-navy md:hover:scale-105">
					See Recent Wins
				</a>
			</div>
		</div>

		<div class={[
			'relative w-full aspect-[16/10] md:aspect-[21/9] overflow-hidden border-2 md:border-4 border-navy transition-all duration-500 md:duration-1000',
			imageVisible ? 'opacity-100 scale-100' : 'opacity-0 scale-95'
		]}>
			<!-- Hero Image -->
			<img
				src="https://images.unsplash.com/photo-1486406146926-c627a92ad1ab?w=1920&q=80"
				alt="Modern corporate skyline representing institutional excellence"
				class="absolute inset-0 w-full h-full object-cover"
				loading="eager"
			/>

			<!-- Subtle overlay for depth -->
			<div class="absolute inset-0 bg-gradient-to-t from-navy/70 via-navy/20 to-transparent"></div>

			<!-- Content overlay with classic styling -->
			<div class="absolute inset-0 flex items-end justify-start p-4 md:p-10">
				<div class={[
					'inline-block border-2 border-gold bg-navy/80 backdrop-blur-sm px-4 py-2 md:px-8 md:py-4 text-cream text-xs md:text-sm font-sans uppercase tracking-wide font-semibold transition-all duration-500 md:duration-1000',
					overlayVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'
				]}>
					Advisory-Grade Demand Generation
				</div>
			</div>
		</div>
	</div>
</section>
