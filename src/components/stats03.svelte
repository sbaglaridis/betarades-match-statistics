<script>
  import Tabs from './tabs.svelte';

  export let label;
  export let stats;
  export let key;

  const tabs = [
    [
      { 'key': 'ou25', 'value': '2.5' },
      { 'key': 'ou15', 'value': '1.5' },
      { 'key': 'ou35', 'value': '3.5' },
    ],
    [
      { 'key': 'f', 'value': 'ΤΕΛ' },
      { 'key': 'fh', 'value': '1ο ΗΜ' },
      { 'key': 'sh', 'value': '2ο ΗΜ' },
    ]
  ];

  let show_state = tabs[0][0].key
  let show_rows = tabs[1][0].key
</script>

<div class="preview-stats" id={ key }>
    {#if label }
        <div class="preview-stats__title">{ label }</div>
    {/if}

    <div class="d-md-flex justify-content-between align-items-center mb-3">
        <Tabs tabs={ tabs[0] } show={ show_state } on:tab={ msg => show_state = msg.detail } className="mb-3 mb-md-0"/>
        <Tabs tabs={ tabs[1] } show={ show_rows } on:tab={ msg => show_rows = msg.detail }/>
    </div>

    <div class="preview-stats__scrollbar">
        <table class="preview-stats__table">
            <thead>
            <tr>
                <th>&nbsp;</th>
                <th colspan="3">ΣΥΝΟΛΟ</th>
                <th colspan="3">ΕΝΤΟΣ</th>
                <th colspan="3">ΕΚΤΟΣ</th>
            </tr>
            <tr>
                <th class="stats-left">ΟΜΑΔΑ</th>
                <th class="stats-col-5 no-wrap">ΑΓΩΝΕΣ</th>
                <th class="stats-col-5 no-wrap">OVER</th>
                <th class="stats-col-5 no-wrap">UNDER</th>
                <th class="stats-col-5 no-wrap">ΑΓΩΝΕΣ</th>
                <th class="stats-col-5 no-wrap">OVER</th>
                <th class="stats-col-5 no-wrap">UNDER</th>
                <th class="stats-col-5 no-wrap">ΑΓΩΝΕΣ</th>
                <th class="stats-col-5 no-wrap">OVER</th>
                <th class="stats-col-5 no-wrap">UNDER</th>
            </tr>
            </thead>
            <tbody>
                {#each Object.keys(stats) as key}
                    {#if key === `${show_state}${show_rows}`}
                        {#each stats[key] as value}
                            <tr>
                                <td>{ value.teamName ?? '' }</td>
                                <td><div class="stats-bordered">{ value.totalOverUnder ?? '' }</div></td>
                                <td><div class="stats-bordered">{ value.totalOver ?? '' }</div></td>
                                <td><div class="stats-bordered">{ value.totalUnder ?? '' }</div></td>
                                <td><div class="stats-bordered">{ value.homeOverUnder ?? '' }</div></td>
                                <td><div class="stats-bordered">{ value.homeOver ?? '' }</div></td>
                                <td><div class="stats-bordered">{ value.homeUnder ?? '' }</div></td>
                                <td><div class="stats-bordered">{ value.awayOverUnder ?? '' }</div></td>
                                <td><div class="stats-bordered">{ value.awayOver ?? '' }</div></td>
                                <td><div class="stats-bordered">{ value.awayUnder ?? '' }</div></td>
                            </tr>
                        {/each}
                    {/if}
                {/each}
            </tbody>
        </table>
    </div>
</div>
