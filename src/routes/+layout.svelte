<script>
	import './styles.css';
</script>

<main>
		<slot />
</main>


<style>
main, main > *{
	height: 100vh;
	width: 100vw;
	display: flex;
	justify-content: stretch;
	align-items: stretch;
}


</style>
