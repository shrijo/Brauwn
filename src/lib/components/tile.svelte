<script>
  let children = 0;
  let isRow = true;
  export let editMode = false;
  export let furrow;
</script>

<fieldset class={isRow ? 'row' : 'column'} id={editMode ? 'editable' : ''} style='
border-bottom: {furrow}px inset rgba(0,0,0,0.2);
border-right: {furrow}px inset rgba(0,0,0,0.2);
border-top: {furrow}px solid rgba(255,255,255,0.2);
border-left: {furrow}px solid rgba(255,255,255,0.2);'>
  <legend>{children}
  <button on:click="{() => children += 1}">+</button>
  <button on:click={() => (isRow = !isRow)}>dir</button>
  </legend>
  {#if children > 0}
    {#each {length: children} as _, i}
      <svelte:self editMode={editMode} furrow={furrow}/>
	  {/each}
  {:else}
  {/if}
</fieldset>

<style>
  .row, .column{
    flex-grow: 1;
    display: flex;
    align-self: stretch;
    margin: 0;
    padding: 0;
    transition: 0.5s ease;
  }

  legend{
    display: none;
  }

  #editable{
    border: 1px solid black !important;
    margin: 5px 10px;
  }

  #editable > legend{
    display: block;
  }

  .row{
    flex-direction: row;
  }
  .column{
    flex-direction: column;
  }
</style>