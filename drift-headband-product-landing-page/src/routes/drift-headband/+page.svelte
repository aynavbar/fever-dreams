<svelte:head>
	<title>Drift Headband — Sleep Dynamics</title>
	<meta name="description" content="The Drift Headband is an ultra-slim, breathable headband that uses bone conduction micro-transducers to deliver audio directly to your inner ear." />
	<meta property="og:title" content="Drift Headband — Sleep Dynamics" />
	<meta property="og:description" content="The Drift Headband is an ultra-slim, breathable headband that uses bone conduction micro-transducers to deliver audio directly to your inner ear." />
	<meta property="og:image" content="https://sdynamics.vercel.app/product_og.jpg" />
	<meta name="twitter:card" content="summary_large_image" />
	<meta name="twitter:image" content="https://sdynamics.vercel.app/product_og.jpg" />
</svelte:head>

<script lang="ts">
	import { Activity, Ear, Waves, ChevronLeft, ChevronRight, Redo, Heart } from 'lucide-svelte';
	import FeatureCard from '#lib/components/FeatureCard.svelte';
	import SpecRow from '#lib/components/SpecRow.svelte';
	import Button from '#lib/components/Button.svelte';

	let scrollContainer: HTMLElement;
	let isAtEnd = $state(false);
	let dialogOpen = $state(false);
	let liked = $state(false);
	let beating = $state(false);

	function checkScrollEnd() {
		if (!scrollContainer) return;
		const { scrollLeft, clientWidth, scrollWidth } = scrollContainer;
		isAtEnd = scrollLeft + clientWidth >= scrollWidth - 25;
	}

	function scrollLeft() {
		if (scrollContainer) {
			scrollContainer.scrollBy({ left: -window.innerWidth * 0.8, behavior: 'smooth' });
		}
	}

	function scrollRight() {
		if (scrollContainer) {
			scrollContainer.scrollBy({ left: window.innerWidth * 0.8, behavior: 'smooth' });
		}
	}

	function handleNextOrReset() {
		if (!scrollContainer) return;
		if (isAtEnd) {
			scrollContainer.scrollTo({ left: 0, behavior: 'smooth' });
		} else {
			scrollRight();
		}
	}

	function openDialog() {
		dialogOpen = true;
	}

	function closeDialog() {
		dialogOpen = false;
	}

	function toggleLike() {
		if (!liked) {
			liked = true;
			beating = true;
			setTimeout(() => { beating = false; }, 600);
		} else {
			liked = false;
		}
	}
</script>

<!-- Hero Section -->
<section class="relative h-svh w-full flex items-end justify-start overflow-hidden pb-6 md:pb-8">
	<img src="/hero-bg.jpg" alt="Drift Headband variants" class="absolute inset-0 w-full h-full object-cover" />

	<!-- Gradient Overlay: Rich dark contrast strictly around the bottom text area, fading quickly to clear -->
	<div class="absolute inset-0 bg-linear-to-t from-black/90 via-black/40 via-35% to-transparent"></div>

	<!-- Content -->
	<div class="relative z-10 flex flex-col items-start text-left max-w-7xl mx-auto px-6 w-full">
		<h1 class="text-7xl md:text-9xl font-semibold tracking-tighter text-white mb-1 md:mb-2 leading-none">Drift</h1>
		<p class="text-2xl md:text-4xl font-medium tracking-tight text-white/90 mb-6 max-w-2xl">
			Sound sleep.
		</p>

		<div class="flex flex-col sm:flex-row items-start sm:items-center gap-3 sm:gap-4">
			<Button onclick={openDialog} class="bg-white text-black px-9 py-3.5 text-base md:text-lg">
				Buy now
			</Button>
			<p class="text-white/90 font-medium tracking-tight text-lg ml-1 sm:ml-0">$149</p>
		</div>
	</div>
</section>

<!-- Zero Pressure Section -->
<section class="relative min-h-svh w-full flex items-end justify-center overflow-hidden pb-12 md:pb-16 px-6">
	<img src="/zero-pressure-bg.jpg" alt="Person sleeping on side with Drift headband" class="absolute inset-0 w-full h-full object-cover" />

	<!-- Gradient Overlay: Dark at bottom for text contrast, fading to transparent -->
	<div class="absolute inset-0 bg-linear-to-t from-black/90 via-black/40 via-40% to-transparent"></div>

	<div class="relative z-10 max-w-5xl mx-auto text-center space-y-8">
		<h2 class="text-5xl md:text-7xl font-semibold tracking-tighter text-white">
			Zero Pressure.<br/><span class="text-white/60">Absolute Balance.</span>
		</h2>
		<p class="text-xl md:text-2xl font-medium tracking-tight text-white/90 max-w-3xl mx-auto leading-relaxed">
			Housed in an ultra-slim, breathable acoustic fabric, the device sits completely flush against your head. You can turn, rest, and sleep naturally.
		</p>
	</div>
</section>

<!-- Features Bento Grid -->
<section class="min-h-svh w-full bg-gray-50 px-6 py-24 flex flex-col justify-center">
	<div class="max-w-7xl mx-auto w-full">
		<div class="mb-16 md:mb-24 text-center md:text-left">
			<h2 class="text-5xl md:text-7xl font-semibold tracking-tighter text-black mb-6">
				The Sound Science,<br/>Internalized.
			</h2>
			<p class="text-xl md:text-2xl font-medium text-gray-500 tracking-tight max-w-2xl">
				Achieving premium acoustic fidelity without acoustic isolation required rethinking how we perceive sound.
			</p>
		</div>

		<!-- Bento Grid / Scrollable List on Mobile -->
		<div bind:this={scrollContainer} onscroll={checkScrollEnd} class="flex md:grid md:grid-cols-2 md:grid-rows-2 gap-6 md:gap-8 overflow-x-auto snap-x snap-mandatory pb-8 md:pb-0 hide-scrollbar -mx-6 px-6 md:mx-0 md:px-0" style="scroll-snap-type: x mandatory;">

			<!-- Card 1 -->
			<FeatureCard
				imageSrc="/bento_micro_transducers.jpg"
				imageAlt="Micro Transducers"
				title="Precision Micro-Transducers"
				class="min-h-[70vh] md:min-h-125 md:col-span-1 md:row-span-2"
			>
				Specially tuned, high-density actuators are woven into the headband's temporal zones. These convert standard audio signals into subtle, precise mechanical vibrations.
			</FeatureCard>

			<!-- Card 2 -->
			<FeatureCard
				imageSrc="/bento_direct_cochlea.jpg"
				imageAlt="Direct to Cochlea"
				title="Direct-to-Cochlea"
				class="min-h-[70vh] md:min-h-full"
			>
				Instead of pushing sound waves through the air, vibrations travel safely and silently through your cranial bones directly to your inner ear.
			</FeatureCard>

			<!-- Card 3 -->
			<FeatureCard
				imageSrc="/bento_uncompromised_fidelity.jpg"
				imageAlt="Uncompromised Fidelity"
				title="Uncompromised Fidelity"
				class="min-h-[70vh] md:min-h-full"
			>
				Advanced equalization algorithms compensate for bone density transfer, preserving the deep, resonant bass and crisp highs of industry-leading in-ear monitors.
			</FeatureCard>

		</div>

		<!-- Mobile Only Navigation Buttons Below Cards -->
		<div class="flex gap-4 justify-center mt-8 md:hidden">
			<button onclick={scrollLeft} class="p-4 rounded-full border border-gray-200 bg-white hover:bg-gray-50 transition-colors shadow-sm focus:outline-none" aria-label="Previous feature">
				<ChevronLeft size={28} strokeWidth={1.5} class="text-black" />
			</button>
			<button onclick={handleNextOrReset} class="p-4 rounded-full border border-gray-200 bg-white hover:bg-gray-50 transition-colors shadow-sm focus:outline-none" aria-label={isAtEnd ? "Reset to beginning" : "Next feature"}>
				{#if isAtEnd}
					<Redo size={28} strokeWidth={1.5} class="text-black" />
				{:else}
					<ChevronRight size={28} strokeWidth={1.5} class="text-black" />
				{/if}
			</button>
		</div>
	</div>
</section>

<!-- Specs Section -->
<section id="buy" class="min-h-svh w-full bg-white px-6 py-24 flex items-center">
	<div class="max-w-5xl mx-auto w-full">
		<h2 class="text-5xl md:text-7xl font-semibold tracking-tighter text-black mb-16 text-center md:text-left">
			Technical Specifications
		</h2>

		<div class="border-t border-gray-200">
			<!-- Spec row -->
			<SpecRow title="Audio Technology">
				Dual High-Density Osteophonic Transducers, Adaptive Bone-Density Equalization (EQ)
			</SpecRow>

			<SpecRow title="Connectivity">
				Bluetooth 5.4 with seamless Multipoint Connection
			</SpecRow>

			<SpecRow title="Battery Life">
				Up to 18 hours of continuous playback; 10-minute quick charge for 4 hours of listening
			</SpecRow>

			<SpecRow title="Materials">
				Antimicrobial, highly breathable acoustic mesh exterior; ultra-flexible memory-titanium core
			</SpecRow>

			<SpecRow title="Weight & Care">
				45 grams. Removable, machine-washable outer sleeve; IPX4 sweat and splash resistant
			</SpecRow>

			<SpecRow title="Smart Features">
				On-head detection for auto-play/pause; Integrated sleep-phase tracking sensors. Low-profile tactile touch-strip for volume and playback.
			</SpecRow>
		</div>
	</div>
</section>

<!-- Final CTA Section -->
<section class="w-full bg-gray-50 px-6 py-32 flex flex-col items-center justify-center text-center border-t border-gray-200">
	<h2 class="text-5xl md:text-7xl font-semibold tracking-tighter text-black mb-6">
		Every high, every low.
	</h2>
	<p class="text-xl md:text-2xl font-medium tracking-tight text-gray-500 max-w-2xl mb-12">
		Experience absolute balance and uncompromised fidelity.
	</p>
	<div class="flex flex-col sm:flex-row items-center gap-4">
		<Button onclick={openDialog} class="bg-black text-white px-12 py-4 text-lg shadow-sm">
			Buy now
		</Button>
		<p class="text-gray-900 font-medium tracking-tight text-lg">$149</p>
	</div>
</section>

<!-- Dialog -->
{#if dialogOpen}
	<!-- svelte-ignore a11y_no_static_element_interactions -->
	<div class="fixed inset-0 z-100 flex items-center justify-center bg-black/50 backdrop-blur-sm px-6" onclick={closeDialog} onkeydown={(e) => { if (e.key === 'Escape') closeDialog(); }}>
		<!-- svelte-ignore a11y_no_static_element_interactions -->
		<div class="bg-white rounded-3xl p-10 md:p-14 max-w-md w-full text-center shadow-2xl" onclick={(e) => e.stopPropagation()} onkeydown={() => {}}>
			<p class="text-xl md:text-2xl font-medium tracking-tight text-gray-800 leading-relaxed mb-10">
				Like the product? It's not real though 😢. You <em>can</em> tap the button below ☺️. Thanks for looking at the site
			</p>

			<button
				onclick={toggleLike}
				class="inline-flex items-center gap-3 px-8 py-4 rounded-full border-2 transition-all duration-300 font-semibold tracking-tight text-lg cursor-pointer {liked ? 'bg-red-50 border-red-400 text-red-500' : 'bg-gray-50 border-gray-200 text-gray-600 hover:border-gray-300'}"
			>
				<span class="inline-flex {beating ? 'heartbeat' : ''}">
					{#if liked}
						<Heart size={28} strokeWidth={2} class="text-red-500 fill-red-500" />
					{:else}
						<Heart size={28} strokeWidth={2} class="text-gray-400" />
					{/if}
				</span>
				{liked ? 'Liked' : 'Like'}
			</button>
		</div>
	</div>
{/if}

<style>
	.hide-scrollbar::-webkit-scrollbar {
		display: none;
	}
	.hide-scrollbar {
		-ms-overflow-style: none;
		scrollbar-width: none;
	}

	@keyframes heartbeat {
		0% { transform: scale(1); }
		15% { transform: scale(1.35); }
		30% { transform: scale(1); }
		45% { transform: scale(1.25); }
		60% { transform: scale(1); }
	}

	:global(.heartbeat) {
		animation: heartbeat 0.6s ease-in-out;
	}
</style>
