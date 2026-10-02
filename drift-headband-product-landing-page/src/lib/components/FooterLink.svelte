<script lang="ts">
	let { href, children } = $props();
</script>

<li><a {href} class="hover:text-white transition-colors">{@render children()}</a></li>
