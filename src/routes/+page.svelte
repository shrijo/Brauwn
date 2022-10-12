<script>

let height = 100;
let width = 100;
let radius = 0;
let maxRadius = height/2;
let color = '#ffffff';
let size = 10;
let blur = size*2;
let doubleBlur= blur*2;
let bezel = 0;
let furrow = 0;
let furrowRadius = 0;
let maxBezel = maxRadius/2;
let concave = false;

function calcFurrowRadius() {
	if(radius != 0){
		furrowRadius = radius + furrow;
	} else {
  	furrowRadius = 0;
	};
};

</script>


<div class="wrapper">
	<div id="content">
		<a href="/button">button</a>
		<div style="
			padding: {furrow}px;
			border-radius: {((radius > 0) ? radius+furrow : 0)}px;
			background: linear-gradient(145deg, rgba(0,0,0,0.08), rgba(0,0,0,0.12));
			box-shadow: 
				2px 2px 4px rgba(255,255,255,0.25),
				inset 2px 2px 4px rgba(0,0,0,0.1),
				0px 0px {doubleBlur}px rgba(0,0,0,0.15), 
				-{size}px -{size}px {blur}px rgba(255,255,255,0.8), 
				{size}px {size}px {blur}px rgba(0,0,0,0.08);
		">
		<div id="element" style="
			margin: {furrow}px;
			box-sizing: border-box;
			border-style: solid;
			border-width: {bezel}px;
			border-color: rgba(0,0,0,0);
			background:
				linear-gradient({concave ? '145deg' : '325deg'}, rgba(0,0,0,0.1), rgba(255,255,255,0.5)) padding-box,
				linear-gradient({color} 0 0) padding-box,
				linear-gradient(145deg, rgba(255,255,255,0.5), rgba(0,0,0,0.1)) border-box,
				linear-gradient({color} 0 0) border-box,
				radial-gradient(#e66465, #9198e5);
			height: {height}px; 
			width: {width}px;
			border-radius: {radius}px;				
			"
		></div>
		</div>
	</div>
	<div id="sidebar">
		<label>height</label>
		<input type="text" bind:value={height}/>
		<label>width</label>
		<input type="text" bind:value={width}/>
		<label>concave</label>
		<input type="checkbox" bind:checked={concave}/><p>{#if concave}yes{:else}no{/if}</p>
		<label>radius</label>
		<input type="range" min="0" max="{maxRadius}" bind:value={radius} />
		<label>color</label>
		<input type="color" bind:value={color}/><p>{color}</p>
		<label>size</label>
		<input type="range" min="2" max="{maxRadius}" bind:value={size}/>
		<label>bezel</label>
		<input type="range" min="0" max="10" bind:value={bezel}/>
		<label>furrow</label>
		<input type="range" min="0" max="10" bind:value={furrow} />
		{radius + furrow}

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
		background-color: #efefef;
		flex-direction: row;
		justify-content: center;
		align-items: center;
	}
	#sidebar{
		padding: 20px;
		height: 100vh;
		width: 100vw;
		background-color: #fff;
		max-width: 300px;
		display: flex;
		flex-direction: column;
	}

	#sidebar > *{
		margin-bottom: 10px;
	}

</style>
