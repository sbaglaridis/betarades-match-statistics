<script>
  import env from "../../env.js"

  import Tabs from './tabs.svelte';
  import TeamBlock from './teamBlock.svelte';

  export let label;
  export let viewport;
  export let info;
  export let stats;
  export let key;

  const tabs = [
    [
      { 'key': 'ha', 'value': 'ΕΝΤΟΣ/ΕΚΤΟΣ' },
      { 'key': 'all', 'value': 'ΣΥΝΟΛΟ' },
    ],
    [
      { 'key': 'n6', 'value': '6' },
      { 'key': 'n10', 'value': '10' },
    ],
    [
      { 'key': info.homeTeam.id, 'value': info.homeTeam.name },
      { 'key': info.awayTeam.id, 'value': info.awayTeam.name },
    ]
  ];

  let show_state = tabs[0][0].key
  let show_rows = tabs[1][0].key
  let show_team = tabs[2][0].key
</script>

<div class="preview-stats" id={ key }>
    {#if label }
        <div class="preview-stats__title">{ label }</div>
    {/if}

    <div class="d-md-flex justify-content-between align-items-center mb-3">
        <Tabs tabs={ tabs[0] } show={ show_state } on:tab={ msg => show_state = msg.detail } className="mb-3 mb-md-0"/>
        <Tabs tabs={ tabs[1] } show={ show_rows } on:tab={ msg => show_rows = msg.detail }/>
    </div>

    {#if viewport !== 'desktop' }
        <div class="mb-3">
            <Tabs tabs={ tabs[2] } show={ show_team } on:tab={ msg => show_team = msg.detail }/>
        </div>
    {/if}

    <div class="row">
        {#each Object.keys(info) as team}
            {#if viewport === 'desktop' || show_team === info[team].id}
                <div class={ viewport === 'desktop' ? 'col-6' : 'col-12' }>
                    <table class="preview-stats__table">
                        <thead>
                            <tr>
                                <th colspan="3">
                                    <TeamBlock
                                        src="{env.TEAM_CDN}/{ info[team].id }.png"
                                        label={ info[team].name }
                                    />
                                </th>
                            </tr>
                            <tr>
                                <th>&nbsp;</th>
                                <th class="stats-col-5 no-wrap">ΗΜ</th>
                                <th class="stats-col-5 no-wrap">ΤΕΛ</th>
                            </tr>
                        </thead>
                        <tbody>
                            {#if show_state === 'ha'}
                                {#each stats[team][team === 'homeTeam' ? 'h10' : 'a10'] ?? [] as row}
                                    <tr>
                                        <td>
                                            <div>{row.matchDateTime}</div>
                                            <div>{row.matchName.split(' - ')[0]}</div>
                                            <div>{row.matchName.split(' - ')[1]}</div>
                                        </td>
                                        <td class="no-wrap"><div class="stats-bordered">{row.htScore}</div></td>
                                        <td class="no-wrap"><div class="stats-bordered">{row.ftScore}</div></td>
                                    </tr>
                                {/each}
                            {/if}
                            {#if show_state === 'all'}
                                {#each stats[team][team === 'homeTeam' ? 'ha10' : 'ah10'] as row}
                                    <tr>
                                        <td>
                                            <div>{row.matchDateTime}</div>
                                            <div>{row.matchName.split(' - ')[0]}</div>
                                            <div>{row.matchName.split(' - ')[1]}</div>
                                        </td>
                                        <td class="no-wrap"><div class="stats-bordered">{row.htScore}</div></td>
                                        <td class="no-wrap"><div class="stats-bordered">{row.ftScore}</div></td>
                                    </tr>
                                {/each}
                            {/if}
                        </tbody>
                    </table>
                </div>
            {/if}
        {/each}
    </div>
</div>
