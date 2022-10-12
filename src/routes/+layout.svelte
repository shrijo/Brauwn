<script>
	import './styles.css';
</script>

<main>
		<slot />
</main>


<style>
main{
	height: 100vh;
	width: 100vw;
}

main > *{
	width: 100vw;
	height: 100vh;
}

</style>
