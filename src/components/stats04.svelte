<script>
  import Tabs from './tabs.svelte';

  export let label;
  export let stats;
  export let key;

  const tabs = [
    [
      { 'key': 'ha', 'value': 'ΕΝΤΟΣ/ΕΚΤΟΣ' },
      { 'key': 't', 'value': 'ΣΥΝΟΛΟ' },
    ]
  ];

  let show_state = tabs[0][0].key
</script>

<div class="preview-stats" id={ key }>
    {#if label }
        <div class="preview-stats__title">{ label }</div>
    {/if}

    <div class="d-flex justify-content-between align-items-center mb-3">
        <Tabs tabs={ tabs[0] } show={ show_state } on:tab={ msg => show_state = msg.detail }/>
    </div>

    <div class="preview-stats__scrollbar">
        <table class="preview-stats__table">
            <thead>
                <tr>
                    <th class="stats-left">ΟΜΑΔΑ</th>
                    <th class="stats-col-5 no-wrap">ΑΓ.</th>
                    <th class="stats-col-5 no-wrap">GG</th>
                    <th class="stats-col-5 no-wrap">NG</th>
                    <th class="stats-col-5 no-wrap">0-1</th>
                    <th class="stats-col-5 no-wrap">2-3</th>
                    <th class="stats-col-5 no-wrap">4-6</th>
                    <th class="stats-col-5 no-wrap">7+</th>
                    <th class="stats-col-5 no-wrap">1 ΗΜ</th>
                    <th class="stats-col-5 no-wrap">Χ ΗΜ</th>
                    <th class="stats-col-5 no-wrap">2 ΗΜ</th>
                </tr>
            </thead>
            <tbody>
                {#each Object.keys(stats) as key}
                    {#if key === show_state}
                        {#each stats[key] as value}
                            <tr>
                                <td class="team label">
                                    <em>{ value.teamName ?? '' }</em>
                                    <span>(&nbsp;{ key === 0 ? 'εντός' : 'εκτός' }&nbsp;)</span>
                                </td>
                                <td><div class="stats-bordered">{ value.played ?? '' }</div></td>
                                <td><div class="stats-bordered">{ value.goalGoal ?? '' }</div></td>
                                <td><div class="stats-bordered">{ value.noGoal ?? '' }</div></td>
                                <td><div class="stats-bordered">{ value.goals01 ?? '' }</div></td>
                                <td><div class="stats-bordered">{ value.goals23 ?? '' }</div></td>
                                <td><div class="stats-bordered">{ value.goals46 ?? '' }</div></td>
                                <td><div class="stats-bordered">{ value.goals7 ?? '' }</div></td>
                                <td><div class="stats-bordered">{ value.winsHt ?? '' }</div></td>
                                <td><div class="stats-bordered">{ value.drawsHt ?? '' }</div></td>
                                <td><div class="stats-bordered">{ value.losesHt ?? '' }</div></td>
                            </tr>
                        {/each}
                    {/if}
                {/each}
            </tbody>
        </table>
    </div>
</div>
