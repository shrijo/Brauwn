<script>
	import './styles.css';
	let innerWidth;
	let innerHeight;
</script>

<svelte:window bind:innerWidth={innerWidth} bind:innerHeight={innerHeight}/>

<main style='height: {innerHeight}; width: {innerWidth}'>
		<slot />
</main>


<style>
main, main > *{
	display: flex;
	justify-content: stretch;
	align-items: stretch;
}


</style>
