<script>
  import Tabs from './tabs.svelte';

  export let label;
  export let stats;
  export let key;
</script>

<div class="preview-stats" id={ key }>
    {#if label }
        <div class="preview-stats__title">{ label }</div>
    {/if}

    <div class="preview-stats__scrollbar">
        <table class="preview-stats__table">
            <thead>
                <tr>
                    <th class="stats-left">ΟΜΑΔΑ</th>
                    <th class="stats-col-5 no-wrap">ΑΓ.</th>
                    <th class="stats-col-5 no-wrap">1/1</th>
                    <th class="stats-col-5 no-wrap">X/1</th>
                    <th class="stats-col-5 no-wrap">2/1</th>
                    <th class="stats-col-5 no-wrap">1/X</th>
                    <th class="stats-col-5 no-wrap">X/X</th>
                    <th class="stats-col-5 no-wrap">2/X</th>
                    <th class="stats-col-5 no-wrap">1/2</th>
                    <th class="stats-col-5 no-wrap">X/2</th>
                    <th class="stats-col-5 no-wrap">2/2</th>
                </tr>
            </thead>
            <tbody>
                {#each Object.keys(stats) as key}
                    {#each stats[key] as value}
                        <tr>
                            <td class="team label">
                                <em>{ value.teamName ?? '' }</em>
                                <span>(&nbsp;{ key === 0 ? 'εντός' : 'εκτός' }&nbsp;)</span>
                            </td>
                            <td><div class="stats-bordered">{ value.played ?? ''}</div></td>
                            <td><div class="stats-bordered">{ value.winWin ?? ''}</div></td>
                            <td><div class="stats-bordered">{ value.drawWin ?? ''}</div></td>
                            <td><div class="stats-bordered">{ value.loseWin ?? ''}</div></td>
                            <td><div class="stats-bordered">{ value.winDraw ?? ''}</div></td>
                            <td><div class="stats-bordered">{ value.drawDraw ?? ''}</div></td>
                            <td><div class="stats-bordered">{ value.loseDraw ?? ''}</div></td>
                            <td><div class="stats-bordered">{ value.winLose ?? ''}</div></td>
                            <td><div class="stats-bordered">{ value.drawLose ?? ''}</div></td>
                            <td><div class="stats-bordered">{ value.loseLose ?? ''}</div></td>
                        </tr>
                    {/each}
                {/each}
            </tbody>
        </table>
    </div>
</div>
