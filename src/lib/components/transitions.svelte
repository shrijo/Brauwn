<script>
  import {slide} from 'svelte/transition';
  export let url: URL;
</script>

{#key url}
  <div in:slide>
    <slot />
  </div>
{/key}

