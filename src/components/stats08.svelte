<script>
  import env from "../../env.js"

  import Tabs from './tabs.svelte';
  import TeamBlock from './teamBlock.svelte';

  export let label;
  export let viewport;
  export let info;
  export let stats;
  export let key;

  const mapping = [
    ['Βαθμοί', 'tPoints', 'hPoints', 'aPoints'],
    ['Αγώνες', 'tPlayed', 'hPlayed', 'aPlayed'],
    ['Νίκες', 'tWins', 'hWins', 'aWins'],
    ['Ισοπαλίες', 'tDraws', 'hDraws', 'aDraws'],
    ['Ήττες', 'tLoses', 'hLoses', 'aLoses'],
    ['Γκόλ Υπέρ', 'tGoalsFor', 'hGoalsFor', 'aGoalsFor'],
    ['Γκόλ Κατά', 'tGoalsAgainst', 'hGoalsAgainst', 'aGoalsAgainst'],
    ['Μ.Ο. γκόλ υπέρ / αγώνα', 'tGoalsForMV', 'hGoalsForMV', 'aGoalsForMV'],
    ['Μ.Ο. γκόλ κατά / αγώνα', 'tGoalsAgainstMV', 'hGoalsAgainstMV', 'aGoalsAgainstMV'],
  ];

  const tabs = [
    { 'key': info.homeTeam.id, 'value': info.homeTeam.name },
    { 'key': info.awayTeam.id, 'value': info.awayTeam.name },
  ]

  let show = tabs[0].key
</script>

<div class="preview-stats" id={ key }>
    {#if label }
        <div class="xpreview-stats__title">{ label }</div>
    {/if}

    {#if viewport !== 'desktop' }
        <div class="mb-3">
            <Tabs { tabs } { show } on:tab={ msg => show = msg.detail }/>
        </div>
    {/if}

    <div class="row">
        {#each Object.keys(info) as team}
            {#if viewport === 'desktop' || show === info[team].id}
                <div class={ viewport === 'desktop' ? 'col-6' : 'col-12' }>
                    <table class="preview-stats__table">
                        <thead>
                            <tr>
                                <th colspan="4">
                                    <TeamBlock
                                        src="{env.TEAM_CDN}/{ info[team].id }.png"
                                        label={ info[team].name }
                                    />
                                </th>
                            </tr>
                            <tr>
                                <th>&nbsp;</th>
                                <th>ΕΝΤΟΣ</th>
                                <th>ΣΥΝΟΛΙΚΑ</th>
                            </tr>
                        </thead>
                        <tbody>
                            {#each stats as item}
                                <tr>
                                    <td>{ item.label}</td>
                                    <td class="stats-col-10">
                                        <div class="stats-bordered">{ team === 'homeTeam' ? item['home'] : item['away'] }</div>
                                    </td>
                                    <td class="stats-col-10">
                                        <div class="stats-bordered">{ team === 'homeTeam' ? item['htotal'] : item['atotal'] }</div>
                                    </td>
                                </tr>
                            {/each}
                        </tbody>
                    </table>
                </div>
            {/if}
        {/each}
    </div>
</div>
