<script lang="ts">
	import { onMount } from 'svelte';

	// Form state using Svelte 5 $state rune
	let formData = $state({
		name: '',
		email: '',
		company: '',
		phone: '',
		message: ''
	});

	let errors = $state({
		name: '',
		email: '',
		company: '',
		message: ''
	});

	let isSubmitting = $state(false);
	let submitSuccess = $state(false);
	let submitError = $state('');

	// Animation states
	let formVisible = $state(false);

	onMount(() => {
		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						setTimeout(() => formVisible = true, 200);
					}
				});
			},
			{ threshold: 0.2 }
		);

		const form = document.getElementById('contact-form');
		if (form) observer.observe(form);

		return () => observer.disconnect();
	});

	function validateEmail(email: string): boolean {
		const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
		return re.test(email);
	}

	function validateForm(): boolean {
		let isValid = true;

		// Reset errors
		errors = {
			name: '',
			email: '',
			company: '',
			message: ''
		};

		// Name validation
		if (!formData.name.trim()) {
			errors.name = 'Name is required';
			isValid = false;
		}

		// Email validation
		if (!formData.email.trim()) {
			errors.email = 'Email is required';
			isValid = false;
		} else if (!validateEmail(formData.email)) {
			errors.email = 'Please enter a valid email address';
			isValid = false;
		}

		// Company validation
		if (!formData.company.trim()) {
			errors.company = 'Company is required';
			isValid = false;
		}

		// Message validation
		if (!formData.message.trim()) {
			errors.message = 'Message is required';
			isValid = false;
		} else if (formData.message.trim().length < 10) {
			errors.message = 'Message must be at least 10 characters';
			isValid = false;
		}

		return isValid;
	}

	async function handleSubmit(event: Event) {
		event.preventDefault();
		submitError = '';
		submitSuccess = false;

		if (!validateForm()) {
			return;
		}

		isSubmitting = true;

		try {
			const response = await fetch('https://formspree.io/f/xaqwwwqn', {
				method: 'POST',
				headers: {
					'Content-Type': 'application/json',
					'Accept': 'application/json'
				},
				body: JSON.stringify(formData)
			});

			if (!response.ok) {
				throw new Error('Form submission failed');
			}

			// Reset form on success
			formData = {
				name: '',
				email: '',
				company: '',
				phone: '',
				message: ''
			};

			submitSuccess = true;

			// Hide success message after 5 seconds
			setTimeout(() => {
				submitSuccess = false;
			}, 5000);
		} catch (error) {
			submitError = 'An error occurred. Please try again.';
		} finally {
			isSubmitting = false;
		}
	}
</script>

<div id="contact-form" class={[
	'max-w-2xl mx-auto transition-all duration-1000',
	formVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'
]}>
	<form onsubmit={handleSubmit} class="space-y-6">
		<!-- Name Field -->
		<div class="transition-all duration-300">
			<label for="name" class="block text-sm font-sans uppercase tracking-wide text-cream mb-2 font-semibold">
				Name <span class="text-gold">*</span>
			</label>
			<input
				type="text"
				id="name"
				bind:value={formData.name}
				class={[
					'w-full px-4 py-3 bg-navy/50 border-2 text-cream placeholder-cream/40 transition-all duration-300',
					'focus:outline-none focus:border-gold focus:bg-navy/70',
					'font-sans',
					errors.name ? 'border-burgundy' : 'border-cream/30 hover:border-cream/50'
				]}
				placeholder="Your full name"
			/>
			{#if errors.name}
				<p class="mt-1 text-sm text-burgundy font-sans">{errors.name}</p>
			{/if}
		</div>

		<!-- Email Field -->
		<div class="transition-all duration-300">
			<label for="email" class="block text-sm font-sans uppercase tracking-wide text-cream mb-2 font-semibold">
				Email <span class="text-gold">*</span>
			</label>
			<input
				type="email"
				id="email"
				bind:value={formData.email}
				class={[
					'w-full px-4 py-3 bg-navy/50 border-2 text-cream placeholder-cream/40 transition-all duration-300',
					'focus:outline-none focus:border-gold focus:bg-navy/70',
					'font-sans',
					errors.email ? 'border-burgundy' : 'border-cream/30 hover:border-cream/50'
				]}
				placeholder="your.email@company.com"
			/>
			{#if errors.email}
				<p class="mt-1 text-sm text-burgundy font-sans">{errors.email}</p>
			{/if}
		</div>

		<!-- Company Field -->
		<div class="transition-all duration-300">
			<label for="company" class="block text-sm font-sans uppercase tracking-wide text-cream mb-2 font-semibold">
				Company <span class="text-gold">*</span>
			</label>
			<input
				type="text"
				id="company"
				bind:value={formData.company}
				class={[
					'w-full px-4 py-3 bg-navy/50 border-2 text-cream placeholder-cream/40 transition-all duration-300',
					'focus:outline-none focus:border-gold focus:bg-navy/70',
					'font-sans',
					errors.company ? 'border-burgundy' : 'border-cream/30 hover:border-cream/50'
				]}
				placeholder="Your company name"
			/>
			{#if errors.company}
				<p class="mt-1 text-sm text-burgundy font-sans">{errors.company}</p>
			{/if}
		</div>

		<!-- Phone Field (Optional) -->
		<div class="transition-all duration-300">
			<label for="phone" class="block text-sm font-sans uppercase tracking-wide text-cream mb-2 font-semibold">
				Phone <span class="text-cream/60 text-sm font-normal">(Optional)</span>
			</label>
			<input
				type="tel"
				id="phone"
				bind:value={formData.phone}
				class={[
					'w-full px-4 py-3 bg-navy/50 border-2 border-cream/30 text-cream placeholder-cream/40 transition-all duration-300',
					'focus:outline-none focus:border-gold focus:bg-navy/70 hover:border-cream/50',
					'font-sans'
				]}
				placeholder="+1 (555) 000-0000"
			/>
		</div>

		<!-- Message Field -->
		<div class="transition-all duration-300">
			<label for="message" class="block text-sm font-sans uppercase tracking-wide text-cream mb-2 font-semibold">
				Message <span class="text-gold">*</span>
			</label>
			<textarea
				id="message"
				bind:value={formData.message}
				rows="5"
				class={[
					'w-full px-4 py-3 bg-navy/50 border-2 text-cream placeholder-cream/40 transition-all duration-300',
					'focus:outline-none focus:border-gold focus:bg-navy/70',
					'font-sans resize-none',
					errors.message ? 'border-burgundy' : 'border-cream/30 hover:border-cream/50'
				]}
				placeholder="Tell us about your pipeline challenges and what you're looking to achieve..."
			></textarea>
			{#if errors.message}
				<p class="mt-1 text-sm text-burgundy font-sans">{errors.message}</p>
			{/if}
		</div>

		<!-- Submit Button -->
		<div class="pt-4">
			<button
				type="submit"
				disabled={isSubmitting}
				class={[
					'w-full bg-gold text-navy px-10 py-5 text-sm font-sans uppercase font-bold tracking-wide',
					'transition-all duration-300 border-2 border-gold',
					'hover:bg-cream hover:border-cream hover:scale-105',
					'disabled:opacity-50 disabled:cursor-not-allowed disabled:hover:scale-100',
					'inline-flex items-center justify-center gap-2'
				]}
			>
				{#if isSubmitting}
					<span>Submitting...</span>
				{:else}
					<span>Submit Inquiry</span>
					<svg width="12" height="12" viewBox="0 0 12 12" fill="none" xmlns="http://www.w3.org/2000/svg">
						<path d="M1 11L11 1M11 1H3M11 1V9" stroke="currentColor" stroke-width="1.5"/>
					</svg>
				{/if}
			</button>
		</div>

		<!-- Success Message -->
		{#if submitSuccess}
			<div class="mt-4 p-4 bg-forest/50 border-2 border-gold text-cream text-base font-sans text-center transition-all duration-500">
				Thank you for your inquiry. We'll be in touch shortly.
			</div>
		{/if}

		<!-- Error Message -->
		{#if submitError}
			<div class="mt-4 p-4 bg-burgundy/50 border-2 border-burgundy text-cream text-base font-sans text-center transition-all duration-500">
				{submitError}
			</div>
		{/if}
	</form>
</div>
