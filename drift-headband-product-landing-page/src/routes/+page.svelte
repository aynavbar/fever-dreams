<script lang="ts">
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';

	onMount(() => {
		goto('/drift-headband', { replaceState: true });
	});
</script>

<svelte:head>
	<title>Sleep Dynamics</title>
	<meta name="description" content="Discover Sleep Dynamics. Experience the future of sleep technology with our innovative devices designed to balance comfort and acoustic perfection." />

	<meta property="og:title" content="Sleep Dynamics" />
	<meta property="og:description" content="Discover Sleep Dynamics. Experience the future of sleep technology with our innovative devices designed to balance comfort and acoustic perfection." />
	<meta property="og:image" content="https://sdynamics.vercel.app/home_og.png" />

	<meta name="twitter:card" content="summary_large_image" />
	<meta name="twitter:title" content="Sleep Dynamics" />
	<meta name="twitter:description" content="Discover Sleep Dynamics. Experience the future of sleep technology with our innovative devices designed to balance comfort and acoustic perfection." />
	<meta name="twitter:image" content="https://sdynamics.vercel.app/home_og.png" />

	<!-- Fallback for non-JS environments or crawlers -->
	<meta http-equiv="refresh" content="0;url=/drift-headband" />
</svelte:head>

<div class="min-h-svh w-full flex items-center justify-center bg-white text-black">
	<p class="text-gray-500 font-medium tracking-tight">Redirecting to Drift Headband...</p>
</div>
