<script>
  import {fly} from 'svelte/transition'
	import { CircleBufferGeometry, TorusKnotGeometry, Mesh, MeshStandardMaterial, Float32BufferAttribute, Vector3, BufferGeometry, PointsMaterial, DoubleSide, Object3D, Points } from 'three'
  import { DEG2RAD } from 'three/src/math/MathUtils'
  import {
    AmbientLight,
    Canvas,
    DirectionalLight,
    Group,
    HemisphereLight,
    OrbitControls,
		Object3DInstance,
    PerspectiveCamera
  } from '@threlte/core'
  import { spring } from 'svelte/motion'

  const scale = spring(1)

 /* -- */
const geometry = new TorusKnotGeometry(4, 1.3, 100, 16);
const torusKnot = new Mesh(geometry);

const sampler = new MeshSurfaceSampler(torusKnot).build();

const vertices = [];
const tempPosition = new Vector3();
for (let i = 0; i < 15000; i ++) {
  sampler.sample(tempPosition);
  vertices.push(tempPosition.x, tempPosition.y, tempPosition.z);
}

const pointsGeometry = new BufferGeometry();
pointsGeometry.setAttribute('position', new Float32BufferAttribute(vertices, 3));
const pointsMaterial = new PointsMaterial({
  color: 0xff61d5,
  size: 0.03
});
const points = new Points(pointsGeometry, pointsMaterial);
 /* -- */

  let sideBar = false;

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
    <div class="canvasWrapper">
		  <Canvas>
				<PerspectiveCamera position={{ x: 10, y: 10, z: 10 }} fov={24}>
					<OrbitControls
						maxPolarAngle={DEG2RAD * 80}
						autoRotate={false}
						enableZoom={false}
						target={{ y: 0.5 }}
					/>
				</PerspectiveCamera>

				<DirectionalLight shadow position={{ x: 3, y: 10, z: 10 }} />
				<DirectionalLight position={{ x: -3, y: 10, z: -10 }} intensity={0.2} />
				<AmbientLight intensity={0.2} />

					<Mesh
						interactive
						on:pointerenter={() => ($scale = 2)}
						on:pointerleave={() => ($scale = 1)}
						position={{ y: 0.5 }}
						castShadow
						geometry={new BoxBufferGeometry(1, 1, 1)}
						material={new MeshStandardMaterial({ color: '#333333' })}
					/>

					<Object3DInstance {object} position={{ y: 1 }} />

			</Canvas>
			
    </div>
		<div id="contentBottombar"></div>
	</div>

	<div id="sidebar" class="{sideBar ? 'shown' : 'hidden'}">
		<h2>3D</h2>

		<fieldset>
		<label>Color</label>
		<input type="color"/>
		</fieldset>

    <fieldset>
		<label>Width</label>
		<input type="range" min="0" max="2" step="0.01" />
		</fieldset>

    <fieldset>
		<label>Height </label>
		<input type="range" min="0" max="2" step="0.01" />
		</fieldset>

    <fieldset>
		<label>Depth</label>
		<input type="range" min="0" max="2" step="0.01"/>
		</fieldset>

		<fieldset>
		<label for="models">Choose a model</label>
		<select id="models" name="models" >
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