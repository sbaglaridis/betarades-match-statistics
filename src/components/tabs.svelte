<script>
  import { createEventDispatcher } from 'svelte';

  export let tabs;
  export let show;
  export let className;

  const dispatch = createEventDispatcher();
</script>

<div class="preview-stats__tabs {className ?? ''}" >
    <ul class="preview-stats__tabs-list">
        {#each tabs as tab}
            <li
                class="preview-stats__tabs-item"
                class:active={show === tab.key}
                on:click={ () => dispatch("tab", tab.key) }
            >
                { tab.value }
            </li>
        {/each}
    </ul>
</div>
