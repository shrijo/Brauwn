<script>
	import { fly } from  'svelte/transition'
</script>


<div in:fly={{x: -200, duration: 500, delay: 500}} out:fly={{x: -200, duration: 500}} class="wrapper">
	<div id="content">
		<a href="/button">button</a>
	</div>
</div>

<style>
	.wrapper{
		height: 100vh;
		width: 100vw;
		display: flex;
		flex-direction: row;
	}
	#content{
		flex-grow: 1;
		display: flex;
		height: 100vh;
		flex-direction: row;
		justify-content: center;
		align-items: center;
	}
</style>
