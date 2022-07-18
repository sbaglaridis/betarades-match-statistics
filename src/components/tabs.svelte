<script>
  export let info;

  let show = info.homeTeam.id

  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  function clickHandler(state) {
    show = state.target.getAttribute('data-team')
    dispatch("tab", show);
  }
</script>

<div class="table-preview-stats__tabs mb-3">
    <ul class="table-preview-stats__tabs-list">
        <li
            class="table-preview-stats__tabs-item"
            class:active={show === info.homeTeam.id}
            data-team={ info.homeTeam.id }
            on:click={ clickHandler }
        >{ info.homeTeam.name }</li>
        <li
            class="table-preview-stats__tabs-item"
            class:active={show === info.awayTeam.id}
            data-team={ info.awayTeam.id }
            on:click={ clickHandler }
        >{ info.awayTeam.name }</li>
    </ul>
</div>
