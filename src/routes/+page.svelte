<script>
	import { fly } from  'svelte/transition'
</script>


<div in:fly={{x: -200, duration: 500, delay: 500}} out:fly={{x: -200, duration: 500}} class="wrapper">
	<div id="content">
		<a href="/button">button</a>
		<a href="/slider">slider</a>
		<a href="/display">display</a>
		<a href="/tiles">tiles</a>
	</div>
</div>

<style>
	.wrapper{
		width: 100vw;
		height: -webkit-fill-available;
		display: flex;
		flex-direction: row;
		align-items: stretch;
	}
	#content{
		flex-grow: 1;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	a{
		text-decoration:none;
		color:black;
		text-transform:uppercase;
		font-weight: 900;
		font-size: 1.8rem;
		transition: 0.5s ease;
	}
	a:hover::before{
		content: '👉';
		font-size: 1.6rem;
		margin: 0 5px;
	}

</style>
