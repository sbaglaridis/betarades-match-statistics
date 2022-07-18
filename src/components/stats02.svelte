<script>
  export let stats;
</script>

<main>
    {#if stats}
        <p>{ stats.homeTeam.teamId} - { stats.awayTeam.teamId}</p>
    {/if}
</main>

<style></style>
