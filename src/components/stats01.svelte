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
        <div class="preview-stats__title">{ label }</div>
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
                                <th>ΣΥΝΟΛΟ</th>
                                <th>ΕΝΤΟΣ</th>
                                <th>ΕΚΤΟΣ</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>Θέση στη βαθμολογία</td>
                                <td>
                                    <div class="stats-bordered">
                                        {(stats.hasOwnProperty(team) && stats[team] != null) ? stats[team].rank : '-'}
                                    </div>
                                </td>
                                <td colspan="2">&nbsp;</td>
                            </tr>
                            {#each mapping as item}
                                <tr>
                                    <td>{ item[0] }</td>
                                    <td class="stats-col-5">
                                        <div class="stats-bordered">{stats[team][item[1]]}</div>
                                    </td>
                                    <td class="stats-col-5">
                                        <div class="stats-bordered">{stats[team][item[2]]}</div>
                                    </td>
                                    <td class="stats-col-5">
                                        <div class="stats-bordered">{stats[team][item[3]]}</div>
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
