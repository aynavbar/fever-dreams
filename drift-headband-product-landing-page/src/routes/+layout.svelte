<script lang="ts">
	import './layout.css';
	import favicon from '#lib/assets/favicon.svg';
	import { Menu, X } from 'lucide-svelte';
	import { slide } from 'svelte/transition';

	let { children } = $props();

	let lastScrollY = $state(0);
	let navbarVisible = $state(true);
	let isTop = $state(true);
	let isMobileMenuOpen = $state(false);

	function handleScroll() {
		if (typeof window === 'undefined') return;
		const currentScrollY = window.scrollY;

		isTop = currentScrollY < 50;

		if (currentScrollY > lastScrollY && currentScrollY > 100) {
			navbarVisible = false;
		} else if (currentScrollY < lastScrollY) {
			navbarVisible = true;
		}
		lastScrollY = currentScrollY;
	}

	function toggleMobileMenu() {
		isMobileMenuOpen = !isMobileMenuOpen;
		if (typeof document !== 'undefined') {
			if (isMobileMenuOpen) {
				document.body.style.overflow = 'hidden';
			} else {
				document.body.style.overflow = '';
			}
		}
	}
</script>

<svelte:window onscroll={handleScroll} />

<svelte:head>
	<title>Drift Headband</title>
	<link rel="icon" href={favicon} />
</svelte:head>

<nav class="fixed top-0 left-0 w-full z-50 transition-all duration-300 ease-in-out border-b {navbarVisible || isMobileMenuOpen ? 'translate-y-0' : '-translate-y-full'} {isMobileMenuOpen ? 'bg-white border-transparent text-black' : isTop ? 'bg-transparent border-transparent text-black' : 'bg-white/90 backdrop-blur-md border-gray-100 text-black'}">
	<div class="max-w-7xl mx-auto px-6 h-16 flex items-center justify-between">
		<a href="/" class="text-lg font-medium tracking-tight">Sleep Dynamics</a>

		<!-- Desktop Links -->
		<div class="hidden md:flex gap-8 items-center text-sm font-medium tracking-tight">
			<a href="/#" class="text-gray-500 hover:text-black transition-colors">Aura Mask</a>
			<a href="/#" class="text-gray-500 hover:text-black transition-colors">Zenith Pillow</a>
			<a href="/drift-headband" class="text-black transition-colors">Drift Headband</a>
		</div>

		<!-- Mobile Menu Toggle -->
		<button class="md:hidden p-2 -mr-2 text-black focus:outline-none" aria-label="Toggle Menu" onclick={toggleMobileMenu}>
			{#if isMobileMenuOpen}
				<X size={24} />
			{:else}
				<Menu size={24} />
			{/if}
		</button>
	</div>
</nav>

<!-- Mobile Menu Overlay -->
{#if isMobileMenuOpen}
	<div transition:slide={{ duration: 400 }} class="fixed inset-0 z-40 bg-white pt-24 px-6 flex flex-col gap-8 text-3xl font-medium tracking-tight md:hidden h-dvh w-full overflow-y-auto">
		<a href="/#" class="text-gray-400 hover:text-black transition-colors" onclick={toggleMobileMenu}>Aura Mask</a>
		<a href="/#" class="text-gray-400 hover:text-black transition-colors" onclick={toggleMobileMenu}>Zenith Pillow</a>
		<a href="/drift-headband" class="text-black transition-colors" onclick={toggleMobileMenu}>Drift Headband</a>
	</div>
{/if}

<main class="bg-white min-h-dvh">
	{@render children()}
</main>

<footer class="bg-black text-white pt-20 pb-10 px-6">
	<div class="max-w-7xl mx-auto grid grid-cols-2 md:grid-cols-4 gap-12 mb-16">
		<div class="col-span-2 md:col-span-1">
			<a href="/" class="text-xl font-medium tracking-tight">Sleep Dynamics</a>
		</div>
		<div>
			<h4 class="font-medium tracking-tight mb-4">Products</h4>
			<ul class="space-y-3 text-sm text-gray-400 font-medium tracking-tight">
				<li><a href="/#" class="hover:text-white transition-colors">Aura Mask</a></li>
				<li><a href="/#" class="hover:text-white transition-colors">Zenith Pillow</a></li>
				<li><a href="/drift-headband" class="hover:text-white transition-colors">Drift Headband</a></li>
			</ul>
		</div>
		<div>
			<h4 class="font-medium tracking-tight mb-4">Company</h4>
			<ul class="space-y-3 text-sm text-gray-400 font-medium tracking-tight">
				<li><a href="/#" class="hover:text-white transition-colors">About Us</a></li>
				<li><a href="/#" class="hover:text-white transition-colors">Careers</a></li>
				<li><a href="/#" class="hover:text-white transition-colors">Press</a></li>
			</ul>
		</div>
		<div>
			<h4 class="font-medium tracking-tight mb-4">Support</h4>
			<ul class="space-y-3 text-sm text-gray-400 font-medium tracking-tight">
				<li><a href="/#" class="hover:text-white transition-colors">Help Center</a></li>
				<li><a href="/#" class="hover:text-white transition-colors">Warranty</a></li>
				<li><a href="/#" class="hover:text-white transition-colors">Contact Us</a></li>
			</ul>
		</div>
	</div>
	<div class="max-w-7xl mx-auto border-t border-white/20 pt-8 flex flex-col md:flex-row justify-between items-center gap-4 text-xs font-medium tracking-tight text-gray-500">
		<p>&copy; 2026 Sleep Dynamics Inc. All rights reserved.</p>
		<div class="flex gap-6">
			<a href="/#" class="hover:text-white transition-colors">Privacy Policy</a>
			<a href="/#" class="hover:text-white transition-colors">Terms of Service</a>
		</div>
	</div>
</footer>
