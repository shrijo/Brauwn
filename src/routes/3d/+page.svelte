<script>
  import {fly} from 'svelte/transition'
	import * as THREE from 'three';
	import * as SC from 'svelte-cubed';
  import Model from '$lib/components/model.svelte'

  let sideBar = false;
	let modelType = 'box';

  let canvasWidth;
  let canvasHeight;

  let color = '0x00ff00';
  let height = '1';
  let width = '1';
  let depth = '1';

</script>


<div in:fly={{x: 200, duration: 500, delay: 500}} out:fly={{x: 200, duration: 500}} class="wrapper">

	<div id="content"  bind:clientWidth={canvasWidth} bind:clientHeight={canvasHeight}>
		<div id="contentTopbar">
			<a href="/" id="backButton">⮕</a>
			<div id="toggleSidebar" on:click={() => (sideBar = !sideBar)} class={sideBar ? 'sidebarOpened' : ''}>
				<div class="plusAround"></div>
				<div class="plusMiddle"></div>
				<div class="plusAround"></div>
			</div>
		</div>
    <div class="canvasWrapper">

		<SC.Canvas antialias alpha>
			{#if modelType == 'gltf'}
			<Model width={width} height={height} depth= {depth}/>
			{:else if modelType == 'box'}
			<SC.Mesh
				geometry={new THREE.BoxGeometry()}
				material={new THREE.MeshStandardMaterial({ color: 0xff3e00 })}
			/>
			{/if}
			<SC.PerspectiveCamera position={[1, 1, 3]} />
			<SC.OrbitControls enableZoom={false} />
			<SC.DirectionalLight intensity={0.6} position={[-2, 3, 2]} />
		​</SC.Canvas>
<!--
		<SC.Canvas antialias alpha height={canvasHeight} width={canvasWidth}>
      <Model width={width} height={height} depth= {depth}/>
      <SC.PerspectiveCamera position={[1, 1, 3]} />
      <SC.OrbitControls enableZoom={false} />
      <SC.AmbientLight intensity={0.6} />
	    <SC.DirectionalLight intensity={0.6} position={[-2, 3, 2]} />
    </SC.Canvas> -->
    </div>
		<div id="contentBottombar"></div>
	</div>

	<div id="sidebar" class="{sideBar ? 'shown' : 'hidden'}">
		<h2>Button</h2>

		<fieldset>
		<label>Color</label>
		<input type="color" bind:value={color}/>
		</fieldset>

    <fieldset>
		<label>Width {width}</label>
		<input type="range" min="0" max="2" step="0.01" bind:value={width}/>
		</fieldset>

    <fieldset>
		<label>Height {height}</label>
		<input type="range" min="0" max="2" step="0.01" bind:value={height}/>
		</fieldset>

    <fieldset>
		<label>Depth {depth}</label>
		<input type="range" min="0" max="2" step="0.01" bind:value={depth}/>
		</fieldset>

		<fieldset>
		<label for="models">Choose a model</label>
		<select id="models" name="models" bind:value={modelType}>
			<option value="box">Cube</option>
			<option value="gltf">GLTF</option>
		</select> 
		</fieldset>

	</div>

</div>


<style>

.canvasWrapper{
  height: 100%;
  width: 100%;
}

.wrapper{
	width: 100vw;
	height: 100vh;
	height: -webkit-fill-available;
	display: flex;
	flex-direction: row;
	align-items: stretch;
}

#content{
	flex-grow: 1;
	display: flex;
	flex-direction: column;
	justify-content: space-between;
	align-items: center;
}

#contentTopbar, #contentBottombar{
	display: flex;
	flex-direction: row;
	justify-content: space-between;
	height: 40px;
	margin: 10px;
	width: calc(100% - 20px);
  z-index: 1000;
}

#backButton{
	text-decoration: none;
	background: white;
	color: black;
	height: 40px;
	min-width: 40px;
	display: flex;
	flex-direction: row;
	justify-content: center;
	align-items: center;
	transform: rotate(-180deg);
}

#toggleSidebar{
	top: 20px;
	right:20px;
	height: 40px;
	width:40px;
	background: #fff;
	border: 0px solid black;
	display:flex;
	flex-direction:column;
	justify-content:center;
	align-items:center;
}

.plusAround{
	width:2px;
	height:5px;
	background: black;
	transition: 0.5s ease;
	transition-delay: 0.5s;
}

.sidebarOpened > .plusAround{
	height:0px;
}

.plusMiddle{
	width:12px;
	height:2px;
	background: black;
}

#sidebar{
	padding: 20px 20px;
	width: 300px;
	background-color: #fff;
	display: flex;
	flex-direction: column;
	transition: 0.2s ease;
  z-index: 1000;
}

.hidden{
	width: 0px !important;
	padding: 0 !important;
	margin: 0 !important;
}

.hidden > *{
	display: none;
}

#sidebar > *{
	margin-bottom: 10px;
}


</style>