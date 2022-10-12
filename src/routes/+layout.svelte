<script>
	import {page} from '$app/stores';
	import Transitions from '$lib/components/transitions.svelte';
	import './styles.css';
</script>

<main>
	<Transitions url={$page.url}>
		<slot />
	</Transitions>
</main>


<style>

</style>
