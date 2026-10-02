<script lang="ts">
	import './layout.css';
	import favicon from '#lib/assets/favicon.svg';
	import { Menu, X } from 'lucide-svelte';
	import { slide } from 'svelte/transition';
	import NavLink from '../lib/components/NavLink.svelte';
	import FooterColumn from '../lib/components/FooterColumn.svelte';
	import FooterLink from '../lib/components/FooterLink.svelte';

	import { dev } from '$app/env';
	import { injectAnalytics } from '@vercel/analytics/sveltekit';

	injectAnalytics({ mode: dev ? 'development' : 'production' });

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

<nav class="fixed top-0 left-0 w-full z-50 transition duration-300 ease-in-out border-b {navbarVisible || isMobileMenuOpen ? 'translate-y-0' : '-translate-y-full'} {isMobileMenuOpen ? 'bg-white border-transparent text-black' : isTop ? 'bg-transparent border-transparent text-black' : 'bg-white/90 backdrop-blur-md border-gray-100 text-black'}">
	<div class="max-w-7xl mx-auto px-6 h-16 flex items-center justify-between">
		<a href="/" class="group flex items-center h-8 md:h-10 w-auto md:w-50 cursor-pointer">
			<div class="relative z-10 shrink-0 flex items-center justify-center">
				<img src={favicon} alt="Logo" class="w-8 h-8 md:w-10 md:h-10 rounded-[0.4rem] md:rounded-xl shadow-sm" />
			</div>
			<div class="relative z-0 overflow-hidden flex-1 h-full flex items-center">
				<span class="pl-3 text-lg font-medium tracking-tight whitespace-nowrap transition-transform duration-500 ease-[cubic-bezier(0.16,1,0.3,1)] md:-translate-x-full md:group-hover:translate-x-0">
					Sleep Dynamics
				</span>
			</div>
		</a>

		<!-- Desktop Links -->
		<div class="hidden md:flex gap-8 items-center text-sm font-medium tracking-tight">
			<NavLink href="/#" class="text-gray-500 hover:text-black">Aura Mask</NavLink>
			<NavLink href="/#" class="text-gray-500 hover:text-black">Zenith Pillow</NavLink>
			<NavLink href="/drift-headband" class="text-black">Drift Headband</NavLink>
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
		<NavLink href="/#" class="text-gray-400 hover:text-black" onclick={toggleMobileMenu}>Aura Mask</NavLink>
		<NavLink href="/#" class="text-gray-400 hover:text-black" onclick={toggleMobileMenu}>Zenith Pillow</NavLink>
		<NavLink href="/drift-headband" class="text-black" onclick={toggleMobileMenu}>Drift Headband</NavLink>
	</div>
{/if}

<main class="bg-white min-h-svh">
	{@render children()}
</main>

<footer class="bg-black text-white pt-20 pb-10 px-6">
	<div class="max-w-7xl mx-auto grid grid-cols-2 md:grid-cols-4 gap-12 mb-16">
		<div class="col-span-2 md:col-span-1">
			<a href="/" class="text-xl font-medium tracking-tight">Sleep Dynamics</a>
		</div>
		<FooterColumn title="Products">
			<FooterLink href="/#">Aura Mask</FooterLink>
			<FooterLink href="/#">Zenith Pillow</FooterLink>
			<FooterLink href="/drift-headband">Drift Headband</FooterLink>
		</FooterColumn>
		<FooterColumn title="Company">
			<FooterLink href="/#">About Us</FooterLink>
			<FooterLink href="/#">Careers</FooterLink>
			<FooterLink href="/#">Press</FooterLink>
		</FooterColumn>
		<FooterColumn title="Support">
			<FooterLink href="/#">Help Center</FooterLink>
			<FooterLink href="/#">Warranty</FooterLink>
			<FooterLink href="/#">Contact Us</FooterLink>
		</FooterColumn>
	</div>
	<div class="max-w-7xl mx-auto border-t border-white/20 pt-8 flex flex-col md:flex-row justify-between items-center gap-4 text-xs font-medium tracking-tight text-gray-500">
		<p>&copy; 2026 Sleep Dynamics Inc. All rights reserved.</p>
		<div class="flex gap-6">
			<a href="/#" class="hover:text-white transition-colors">Privacy Policy</a>
			<a href="/#" class="hover:text-white transition-colors">Terms of Service</a>
		</div>
	</div>
</footer>
