<script lang="ts">
	let { href, class: className = '', onclick = undefined, children } = $props();
</script>

<a {href} class="transition-colors {className}" {onclick}>{@render children()}</a>
