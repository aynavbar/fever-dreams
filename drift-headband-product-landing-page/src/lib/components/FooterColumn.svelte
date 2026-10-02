<script lang="ts">
	let { title, children } = $props();
</script>

<div>
	<h4 class="font-medium tracking-tight mb-4">{title}</h4>
	<ul class="space-y-3 text-sm text-gray-400 font-medium tracking-tight">
		{@render children()}
	</ul>
</div>
