<script>
  import {fly} from 'svelte/transition';
  export let url = "";
</script>

{#key url}
  <div 
  in:fly={{x: 100, duration: 250, delay: 250 }} 
  out:fly={{x: -100, duration: 250}} 
  >
    <slot />
  </div>
{/key}

