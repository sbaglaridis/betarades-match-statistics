<script>
  import Tabs from './tabs.svelte';

  export let team_cdn;
  export let viewport = 'mobile';
  export let info;
  export let stats;

  let mapping = [
    [ 'Βαθμοί', 'tPoints', 'hPoints', 'aPoints' ],
    [ 'Αγώνες', 'tPlayed', 'hPlayed', 'aPlayed' ],
    [ 'Νίκες', 'tWins', 'hWins', 'aWins' ],
    [ 'Ισοπαλίες', 'tDraws', 'hDraws', 'aDraws' ],
    [ 'Ήττες', 'tLoses', 'hLoses', 'aLoses' ],
    [ 'Γκόλ Υπέρ', 'tGoalsFor', 'hGoalsFor', 'aGoalsFor' ],
    [ 'Γκόλ Κατά', 'tGoalsAgainst', 'hGoalsAgainst', 'aGoalsAgainst' ],
    [ 'Μ.Ο. γκόλ υπέρ / αγώνα', 'tGoalsForMV', 'hGoalsForMV', 'aGoalsForMV' ],
    [ 'Μ.Ο. γκόλ κατά / αγώνα', 'tGoalsAgainstMV', 'hGoalsAgainstMV', 'aGoalsAgainstMV' ],
  ];

  let show = info.homeTeam.id

  function handleMessage(msg) {
    show = msg.detail
  }
</script>

<div class="card card--main table-preview-stats">
    <div class="card__title mb-3">Στατιστικά</div>

    {#if viewport !== 'desktop' }
        <Tabs info={ info } on:tab={handleMessage} />
    {/if}

    <div class="row">
        {#each ['homeTeam', 'awayTeam'] as team}
            <div class={ viewport === 'desktop' ? 'col-6' : 'col-12' }>
                {#if viewport === 'desktop' || show === info[team].id}
                    <table class="table-preview-stats__table">
                        <thead>
                            <tr>
                                <th colspan="4">
                                    <div class="table-preview-stats__info stats-top-header-bordered g-16 mb-2">
                                        <div class="table-preview-stats__team-t-short">
                                            <img
                                                src="{team_cdn}/{ info[team].id }.png"
                                                alt="{ info[team].name }"
                                                width="28"
                                                height="28"
                                                loading="lazy"
                                            >
                                        </div>
                                        <div>{ info[team].name }</div>
                                    </div>
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
                                        {(stats.hasOwnProperty(team) && stats[team] != null) ? stats[team].rank : ''}
                                    </div>
                                </td>
                                <td colspan="2">&nbsp;</td>
                            </tr>
                            {#each mapping as item}
                                <tr>
                                    <td>{ item[0] }</td>
                                    <td>
                                        <div class="stats-bordered">{stats[team][item[1]]}</div>
                                    </td>
                                    <td>
                                        <div class="stats-bordered">{stats[team][item[2]]}</div>
                                    </td>
                                    <td>
                                        <div class="stats-bordered">{stats[team][item[3]]}</div>
                                    </td>
                                </tr>
                            {/each}
                        </tbody>
                    </table>
                {/if}
            </div>
        {/each}
    </div>
</div>

<style></style>
