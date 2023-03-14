<script>
  export let index;
  export let binding;
  let width = 0;
</script>

{#if binding}
  <div bind:clientWidth={width}>
    {index}
  </div>
{:else}
  <div>
    {index}
  </div>
{/if}