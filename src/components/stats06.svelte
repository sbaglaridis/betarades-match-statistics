<script>
  import env from "../../env.js"

  export let label;
  export let viewport;
  export let info;
  export let stats;
  export let key;

</script>

<div class="preview-stats" id={ key }>
    {#if label }
        <div class="preview-stats__title">{ label }</div>
    {/if}
</div>
