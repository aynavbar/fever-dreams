<script lang="ts">
	import { Activity, Ear, Waves, ChevronLeft, ChevronRight, Redo, Heart } from 'lucide-svelte';

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
			<button onclick={openDialog} class="bg-white text-black px-9 py-3.5 rounded-full font-semibold tracking-tight text-base md:text-lg hover:scale-105 transition-transform duration-300 cursor-pointer">
				Buy now
			</button>
			<p class="text-white/90 font-medium tracking-tight text-lg ml-1 sm:ml-0">$149</p>
		</div>
	</div>
</section>

<!-- Zero Pressure Section -->
<section class="relative min-h-svh w-full flex items-end justify-center overflow-hidden pb-12 md:pb-16 px-6">
	<img src="/zero-pressure-bg.jpg" alt="Person sleeping on side with Drift headband" class="absolute inset-0 w-full h-full object-cover" />

	<!-- Gradient Overlay: Dark at bottom for text contrast, fading to transparent -->
	<div class="absolute inset-0 bg-gradient-to-t from-black/90 via-black/40 via-40% to-transparent"></div>

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
				The Science of Sound,<br/>Internalized.
			</h2>
			<p class="text-xl md:text-2xl font-medium text-gray-500 tracking-tight max-w-2xl">
				Achieving premium acoustic fidelity without acoustic isolation required rethinking how we perceive sound.
			</p>
		</div>

		<!-- Bento Grid / Scrollable List on Mobile -->
		<div bind:this={scrollContainer} onscroll={checkScrollEnd} class="flex md:grid md:grid-cols-2 md:grid-rows-2 gap-6 md:gap-8 overflow-x-auto snap-x snap-mandatory pb-8 md:pb-0 hide-scrollbar -mx-6 px-6 md:mx-0 md:px-0" style="scroll-snap-type: x mandatory;">

			<!-- Card 1 -->
			<div class="bg-white rounded-[2.5rem] p-10 md:p-12 flex flex-col justify-end min-h-[70vh] md:min-h-125 w-[85vw] md:w-auto shrink-0 snap-center md:col-span-1 md:row-span-2 shadow-sm border border-gray-100/50">
				<div class="mb-auto">
					<Activity size={48} strokeWidth={1.5} class="text-black mb-6" />
				</div>
				<h3 class="text-3xl md:text-4xl font-semibold tracking-tight text-black mb-4">Precision Micro-Transducers</h3>
				<p class="text-lg md:text-xl font-medium text-gray-500 leading-relaxed">
					Specially tuned, high-density actuators are woven into the headband's temporal zones. These convert standard audio signals into subtle, precise mechanical vibrations.
				</p>
			</div>

			<!-- Card 2 -->
			<div class="bg-white rounded-[2.5rem] p-10 md:p-12 flex flex-col justify-end min-h-[70vh] md:min-h-full w-[85vw] md:w-auto shrink-0 snap-center shadow-sm border border-gray-100/50">
				<div class="mb-auto">
					<Ear size={48} strokeWidth={1.5} class="text-black mb-6" />
				</div>
				<h3 class="text-3xl md:text-4xl font-semibold tracking-tight text-black mb-4">Direct-to-Cochlea</h3>
				<p class="text-lg md:text-xl font-medium text-gray-500 leading-relaxed">
					Instead of pushing sound waves through the air, vibrations travel safely and silently through your cranial bones directly to your inner ear.
				</p>
			</div>

			<!-- Card 3 -->
			<div class="bg-black text-white rounded-[2.5rem] p-10 md:p-12 flex flex-col justify-end min-h-[70vh] md:min-h-full w-[85vw] md:w-auto shrink-0 snap-center shadow-sm">
				<div class="mb-auto">
					<Waves size={48} strokeWidth={1.5} class="text-white mb-6" />
				</div>
				<h3 class="text-3xl md:text-4xl font-semibold tracking-tight mb-4">Uncompromised Fidelity</h3>
				<p class="text-lg md:text-xl font-medium text-gray-400 leading-relaxed">
					Advanced equalization algorithms compensate for bone density transfer, preserving the deep, resonant bass and crisp highs of industry-leading in-ear monitors.
				</p>
			</div>

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
			<div class="py-8 border-b border-gray-200 flex flex-col md:flex-row md:items-start gap-4 md:gap-12">
				<h4 class="text-2xl font-semibold tracking-tight text-black md:w-1/3">Audio Technology</h4>
				<p class="text-xl md:text-2xl font-medium text-gray-500 md:w-2/3">Dual High-Density Osteophonic Transducers, Adaptive Bone-Density Equalization (EQ)</p>
			</div>

			<div class="py-8 border-b border-gray-200 flex flex-col md:flex-row md:items-start gap-4 md:gap-12">
				<h4 class="text-2xl font-semibold tracking-tight text-black md:w-1/3">Connectivity</h4>
				<p class="text-xl md:text-2xl font-medium text-gray-500 md:w-2/3">Bluetooth 5.4 with seamless Multipoint Connection</p>
			</div>

			<div class="py-8 border-b border-gray-200 flex flex-col md:flex-row md:items-start gap-4 md:gap-12">
				<h4 class="text-2xl font-semibold tracking-tight text-black md:w-1/3">Battery Life</h4>
				<p class="text-xl md:text-2xl font-medium text-gray-500 md:w-2/3">Up to 18 hours of continuous playback; 10-minute quick charge for 4 hours of listening</p>
			</div>

			<div class="py-8 border-b border-gray-200 flex flex-col md:flex-row md:items-start gap-4 md:gap-12">
				<h4 class="text-2xl font-semibold tracking-tight text-black md:w-1/3">Materials</h4>
				<p class="text-xl md:text-2xl font-medium text-gray-500 md:w-2/3">Antimicrobial, highly breathable acoustic mesh exterior; ultra-flexible memory-titanium core</p>
			</div>

			<div class="py-8 border-b border-gray-200 flex flex-col md:flex-row md:items-start gap-4 md:gap-12">
				<h4 class="text-2xl font-semibold tracking-tight text-black md:w-1/3">Weight & Care</h4>
				<p class="text-xl md:text-2xl font-medium text-gray-500 md:w-2/3">45 grams. Removable, machine-washable outer sleeve; IPX4 sweat and splash resistant</p>
			</div>

			<div class="py-8 border-b border-gray-200 flex flex-col md:flex-row md:items-start gap-4 md:gap-12">
				<h4 class="text-2xl font-semibold tracking-tight text-black md:w-1/3">Smart Features</h4>
				<p class="text-xl md:text-2xl font-medium text-gray-500 md:w-2/3">On-head detection for auto-play/pause; Integrated sleep-phase tracking sensors. Low-profile tactile touch-strip for volume and playback.</p>
			</div>
		</div>
	</div>
</section>

<!-- Final CTA Section -->
<section class="w-full bg-gray-50 px-6 py-32 flex flex-col items-center justify-center text-center border-t border-gray-200">
	<h2 class="text-5xl md:text-7xl font-semibold tracking-tighter text-black mb-6">
		Ready for sound sleep?
	</h2>
	<p class="text-xl md:text-2xl font-medium tracking-tight text-gray-500 max-w-2xl mb-12">
		Experience absolute balance and uncompromised fidelity.
	</p>
	<div class="flex flex-col sm:flex-row items-center gap-4">
		<button onclick={openDialog} class="bg-black text-white px-12 py-4 rounded-full font-semibold tracking-tight text-lg hover:scale-105 transition-transform duration-300 shadow-sm cursor-pointer">
			Buy now
		</button>
		<p class="text-gray-900 font-medium tracking-tight text-lg">$149</p>
	</div>
</section>

<!-- Dialog -->
{#if dialogOpen}
	<!-- svelte-ignore a11y_no_static_element_interactions -->
	<div class="fixed inset-0 z-[100] flex items-center justify-center bg-black/50 backdrop-blur-sm px-6" onclick={closeDialog} onkeydown={(e) => { if (e.key === 'Escape') closeDialog(); }}>
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
