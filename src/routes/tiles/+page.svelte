<script>
import {fly} from 'svelte/transition'
import Tile from '$lib/components/tile.svelte'

let text = '';
let sideBar = false;
let editMode = false;
let furrow = 0;


</script>

<div in:fly={{x: 200, duration: 500, delay: 500}} out:fly={{x: 200, duration: 500}} class="wrapper">

	<div id="content">
		<div id="contentTopbar">
			<a href="/" id="backButton">⮕</a>
			<div id="toggleSidebar" on:click={() => (sideBar = !sideBar)} class={sideBar ? 'sidebarOpened' : ''}>
				<div class="plusAround"></div>
				<div class="plusMiddle"></div>
				<div class="plusAround"></div>
			</div>
		</div>
		<Tile editMode={editMode} furrow={furrow}/>
		<div id="contentBottombar"></div>
	</div>

	<div id="sidebar" class="{sideBar ? 'shown' : 'hidden'}">
		<h2>Button</h2>

		<fieldset>
		<div class="checkboxWrapper">
			<input type="checkbox" name="editMode" bind:checked={editMode} >
			<label class="checkboxLabel" for="editMode">Edit Mode</label>
		</div>
		</fieldset>

		<fieldset>
			<label>Furrow</label>
			<input type="range" min="0" max="5" bind:value={furrow}>
		</fieldset>
		
		{editMode}
	</div>

</div>


<style>

.wrapper{
	height: 100vh;
	height: -webkit-fill-available;
	height: fill-available;
	width: 100vw;
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