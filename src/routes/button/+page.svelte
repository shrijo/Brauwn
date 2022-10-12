<script>

let text = '';
let sideBar = false;

let styles = {
	height: '100',
	width: '100',
	radius: '0',
	bezel: '0',
	furrow: '0',
	bump: '2px 2px 4px rgba(255,255,255,0.25)',
	maxRadius: '0',
	color: '#ffffff',
	size: '10',
	blur: '20',
	surface: 'linear-gradient(rgba(0,0,0,0) 0 0) content-box',
}

$: cssVarStyles = Object.entries(styles)
		.map(([key, value]) => `--${key}:${value}`)
		.join(';');

function toggleSidebar(){
	alert('hello')
}

</script>

<div class="wrapper">

	<div id="content">
		<div id="contentTopbar"><div id="toggleSidebar" on:click={() => (sideBar = !sideBar)}></div></div>
		<button style="{cssVarStyles}">{text}</button>
		<div id="contentBottombar"></div>
	</div>

	<div id="sidebar" class="{sideBar ? 'shown' : 'hidden'}">
		<h2>Button</h2>

		<fieldset>
		<label>text</label>
		<input type="text" bind:value={text}/>
		</fieldset>
		
		<fieldset>
		<label>height</label>
		<input type="text" bind:value={styles['height']}/>
		</fieldset>
		
		<fieldset>
		<label>width</label>
		<input type="text" bind:value={styles['width']}/>
		</fieldset>
		
		<fieldset>
		<label>radius</label>
		<input type="range" min="0" max="{styles['height']/2}" bind:value={styles['radius']} />
		</fieldset>
		
		<fieldset>
		<label>bezel</label>
		<input type="range" min="0" max="{styles['height']/2-10}" bind:value={styles['bezel']} />
		</fieldset>

		<fieldset>
		<label>forrow</label>
		<input type="range" min="0" max="10" bind:value={styles['furrow']} />
		<div class="checkboxWrapper">
			<input type="checkbox" name="bump" checked bind:group={styles['bump']} value={'2px 2px 4px rgba(255,255,255,0.25)'} >
			<label class="checkboxLabel" for="bump">bump</label>
		</div>
		</fieldset>

		<fieldset>
		<label>color</label>
		<div class="row"><input type="color" bind:value={styles['color']}><p style="margin-left: 10px">{styles['color']}</p></div>
		</fieldset>

		<fieldset>
		<div class="radioWrapper">
			<input type="radio" name="surface" bind:group={styles['surface']} value={'linear-gradient(rgba(0,0,0,0) 0 0) content-box'} checked>
			<label class="radioLabel" for="flat">flat</label>
		</div>
		<div class="radioWrapper">
			<input type="radio" name="surface" bind:group={styles['surface']} value={'linear-gradient(145deg, rgba(255,255,255,0.08), rgba(0,0,0,0.1)) content-box'}>
			<label class="radioLabel" for="convex">convex</label>
		</div>
		<div class="radioWrapper">
			<input type="radio" name="surface" bind:group={styles['surface']} value={'linear-gradient(325deg, rgba(255,255,255,0.08), rgba(0,0,0,0.1)) content-box'}>
			<label class="radioLabel" for="concav">concav</label>
		</div>
		</fieldset>
	</div>

</div>


<style>

button{
	border-color: rgba(0,0,0,0);
	border-style: solid;
	box-sizing: border-box;
	border-width: calc(var(--furrow)*1px);
  height: calc(var(--height)*1px);
  min-width: calc(var(--width)*1px);
  border-radius: calc(var(--radius)*1px);
	background:
		var(--surface),
		linear-gradient(var(--color) 0 0) content-box,
		linear-gradient(145deg, rgba(255,255,255,0.08), rgba(0,0,0,0.15)) padding-box,
		linear-gradient(var(--color) 0 0) padding-box,
		radial-gradient(rgba(0,0,0,0.08), rgba(0,0,0,0.25)) border-box;
	padding: calc(var(--bezel)*1px);
	box-shadow: 
				var(--bump),
				0px 0px 20px rgba(0,0,0,0.15), 
				-10px -10px 10px rgba(255,255,255,0.8), 
				10px 10px 10px rgba(0,0,0,0.08);
}

.wrapper{
	height: 100vh;
	width: 100vw;
	display: flex;
	flex-direction: row;
}
#content{
	flex-grow: 1;
	display: flex;
	flex-direction: column;
	height: 100vh;
	background-color: #efefef;
	justify-content: space-between;
	align-items: center;
}

#contentTopbar, #contentBottombar{
	display: flex;
	flex-direction: row-reverse;
	height: 40px;
	margin: 10px;
	width: calc(100% - 20px);
}

#toggleSidebar{
	top: 20px;
	right:20px;
	height: 40px;
	width:40px;
	background: #fff;
	border: 0px solid black;
}

#sidebar{
	padding: 20px 20px;
	height: 100vh;
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