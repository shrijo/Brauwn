<script>
import * as SC from 'svelte-cubed';
import { onMount } from 'svelte';
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js';

let modelURL = 'https://modelviewer.dev/shared-assets/models/NeilArmstrong.glb'
let model = null;

export let width = '1';
export let height = '1';
export let depth = '1';


function loadGLTF() {
  const loader = new GLTFLoader();
  return loader.loadAsync(modelURL)
}

onMount(() => {
  loadGLTF().then(_model => model = _model);
})
</script>


{#if model}
  <SC.Primitive
    object={model.scene}
    scale={[width,height,depth]}
  />
{/if}
