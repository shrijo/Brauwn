<script>
	import './styles.css';
</script>


<main>
		<slot />
</main>


<style>
main, main > *{
	display: flex;
	justify-content: stretch;
	align-items: stretch;
	width: 100vw;
	height: 100%;
}


</style>
