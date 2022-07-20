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

    <div class="preview-stats__scrollbar">
        <table class="preview-stats__table">
            <thead>
                <tr>
                    <th class="no-wrap">Α/Α</th>
                    <th class="stats-left">ΟΜΑΔΑ</th>
                    <th class="stats-col-5">Β</th>
                    <th class="stats-col-5">ΑΓ</th>
                    <th class="stats-col-5">Ν</th>
                    <th class="stats-col-5">Ι</th>
                    <th class="stats-col-5">Η</th>
                    <th class="stats-col-5">ΓΚΟΛ</th>
                    <th class="stats-col-5">ΦΟΡΜΑ &amp;<br/>OVER/UNDER</th>
                </tr>
            </thead>
            <tbody>
                {#each stats as item}
                    <tr>
                        <td class="stats-col-1 stats-center no-wrap legend-{ item.legend }">{ item.rank}</td>
                        <td>{ item.teamName }</td>
                        <td><div class="stats-bordered">{ item.points }</div></td>
                        <td><div class="stats-bordered">{ item.played }</div></td>
                        <td><div class="stats-bordered">{ item.wins }</div></td>
                        <td><div class="stats-bordered">{ item.draws }</div></td>
                        <td><div class="stats-bordered">{ item.loses }</div></td>
                        <td><div class="stats-bordered no-wrap">{ item.goals }</div></td>
                        <td>
                            <div class="d-flex justify-content-between mb-2">
                                {@html item.matchForm.split(',').map(key => `<div class="status ${key}"></div>`).join('') }
                            </div>
                            <div class="d-flex justify-content-between">
                                {@html item.overUnderForm.split(',').map(key => `<div class="status ${key}"></div>`).join('') }
                            </div>
                        </td>
                    </tr>
                {/each}
            </tbody>
        </table>
    </div>
</div>
