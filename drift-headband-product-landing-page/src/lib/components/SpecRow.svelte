<script lang="ts">
	let { title, children } = $props();
</script>

<div class="py-8 border-b border-gray-200 flex flex-col md:flex-row md:items-start gap-4 md:gap-12">
	<h4 class="text-2xl font-semibold tracking-tight text-black md:w-1/3">{title}</h4>
	<div class="text-xl md:text-2xl font-medium text-gray-500 md:w-2/3">
		{@render children()}
	</div>
</div>
