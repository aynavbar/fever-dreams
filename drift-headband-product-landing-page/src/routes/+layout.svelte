<script lang="ts">
	import './layout.css';
	import favicon from '#lib/assets/favicon.svg';

	let { children } = $props();

	let lastScrollY = $state(0);
	let navbarVisible = $state(true);
	let isTop = $state(true);

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
</script>

<svelte:window onscroll={handleScroll} />

<svelte:head>
	<title>Drift Headband</title>
	<link rel="icon" href={favicon} />
</svelte:head>

<nav class="fixed top-0 left-0 w-full z-50 transition-all duration-300 ease-in-out border-b border-transparent {navbarVisible ? 'translate-y-0' : '-translate-y-full'} {isTop ? 'bg-transparent text-black' : 'bg-white/90 backdrop-blur-md border-gray-100'}">
	<div class="max-w-7xl mx-auto px-6 h-16 flex items-center justify-between">
		<a href="/" class="text-lg font-medium tracking-tight">Sleep Dynamics</a>
		<div class="hidden md:flex gap-8 items-center text-sm font-medium tracking-tight">
			<a href="#" class="text-gray-500 hover:text-black transition-colors">Aura Mask</a>
			<a href="#" class="text-gray-500 hover:text-black transition-colors">Zenith Pillow</a>
			<a href="/drift-headband" class="text-black transition-colors">Drift Headband</a>
		</div>
	</div>
</nav>

<main class="bg-white">
	{@render children()}
</main>
