<script lang="ts">
	let { imageSrc, imageAlt, title, children, class: className = '' } = $props();
</script>

<div class="relative bg-gray-100 rounded-[2.5rem] p-3 md:p-6 flex flex-col justify-end w-[85vw] md:w-auto shrink-0 snap-center shadow-sm border border-gray-100/50 overflow-hidden {className}">
	<img src={imageSrc} alt={imageAlt} class="absolute inset-0 w-full h-full object-cover" />
	<div class="absolute inset-0 bg-black/10"></div>

	<div class="relative z-10 bg-white/95 backdrop-blur-xl rounded-4xl p-8 md:p-10 shadow-lg border border-white/50 w-full mt-auto">
		<h3 class="text-3xl md:text-4xl font-semibold tracking-tight text-black mb-4">{title}</h3>
		<div class="text-lg md:text-xl font-medium text-gray-600 leading-relaxed">
			{@render children()}
		</div>
	</div>
</div>
