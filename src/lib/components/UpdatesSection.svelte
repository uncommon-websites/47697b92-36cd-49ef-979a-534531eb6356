<script lang="ts">
	import { onMount } from 'svelte';
	import ContactForm from './ContactForm.svelte';

	let decorativeLineVisible = $state(false);
	let headingVisible = $state(false);
	let descriptionVisible = $state(false);
	let formVisible = $state(false);
	let footerVisible = $state(false);
	let isMobile = $state(false);

	onMount(() => {
		isMobile = window.matchMedia('(max-width: 768px)').matches;

		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						if (isMobile) {
							// Immediate on mobile
							decorativeLineVisible = true;
							headingVisible = true;
							descriptionVisible = true;
							formVisible = true;
							footerVisible = true;
						} else {
							setTimeout(() => decorativeLineVisible = true, 100);
							setTimeout(() => headingVisible = true, 300);
							setTimeout(() => descriptionVisible = true, 600);
							setTimeout(() => formVisible = true, 900);
							setTimeout(() => footerVisible = true, 1200);
						}
					}
				});
			},
			{ threshold: isMobile ? 0.1 : 0.3 }
		);

		const section = document.getElementById('contact');
		if (section) observer.observe(section);

		return () => observer.disconnect();
	});
</script>

<section id="contact" class="py-12 md:py-24 border-b-2 border-navy bg-navy text-cream">
	<div class="container-custom">
		<div class="max-w-3xl mx-auto text-center px-2">
			<div class={[
				'w-16 md:w-24 h-0.5 bg-gold mx-auto mb-4 md:mb-8 transition-all duration-500 md:duration-700',
				decorativeLineVisible ? 'opacity-100 scale-x-100' : 'opacity-0 scale-x-0'
			]}></div>
			<h2 class={[
				'text-2xl sm:text-3xl md:text-5xl font-serif font-bold mb-4 md:mb-8 text-cream leading-tight transition-all duration-500 md:duration-1000',
				headingVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'
			]}>
				Ready to Build Predictable Pipeline?
			</h2>
			<p class={[
				'text-sm sm:text-base md:text-xl text-cream/90 mb-8 md:mb-12 max-w-2xl mx-auto leading-relaxed font-sans transition-all duration-500 md:duration-1000',
				descriptionVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'
			]}>
				We work with a limited number of clients. If you're a B2B executive facing pipeline unpredictability in brand-sensitive markets, let's explore fit.
			</p>

			<div class={[
				'mb-10 md:mb-16 transition-all duration-500 md:duration-1000',
				formVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'
			]}>
				<ContactForm />
			</div>

			<div class={[
				'border-t-2 border-gold/30 pt-6 md:pt-10 transition-all duration-500 md:duration-1000',
				footerVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'
			]}>
				<p class="text-xs md:text-sm text-gold uppercase tracking-wide mb-4 md:mb-6 font-sans font-semibold">Trusted by operators in</p>
				<div class="flex flex-wrap justify-center gap-x-3 gap-y-2 md:gap-8 text-xs sm:text-sm md:text-base text-cream/90 font-sans font-medium">
					<span>Institutional Finance</span>
					<span class="text-gold hidden sm:inline">•</span>
					<span>Private Equity</span>
					<span class="text-gold hidden sm:inline">•</span>
					<span>Enterprise Tech</span>
					<span class="text-gold hidden sm:inline">•</span>
					<span>Professional Services</span>
				</div>
			</div>
		</div>
	</div>
</section>
