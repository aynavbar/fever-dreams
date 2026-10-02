<script lang="ts">
	let { class: className = '', children, onclick, ...rest } = $props();
</script>

<button class="rounded-full font-semibold tracking-tight hover:scale-105 transition-transform duration-300 cursor-pointer {className}" {onclick} {...rest}>
	{@render children()}
</button>
