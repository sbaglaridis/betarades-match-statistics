<script>
  const team_cdn = 'https://www.europaleague.gr/betarades/cdn/teams'

  import { onMount } from 'svelte';
  import State01 from './components/stats01.svelte'

  let stats = null
  let viewport = 'mobile';

  function checkViewport() {
    if (window.innerWidth >= 992) {
      viewport = 'desktop'
    } else if (window.innerWidth >= 576) {
      viewport = 'tablet'
    } else {
      viewport = 'mobile'
    }

    return true
  }

  onMount(() => {
    checkViewport() && window.addEventListener('resize', checkViewport);
  })

  fetch('/data.json')
      .then(response => response.json())
      .then(data => {
        document.querySelector('.block-loader').remove()
        stats = data
      });

  $: console.log('viewport is no:', viewport)

</script>

<main>
  {#if stats && stats.stats01}
    <State01
        viewport={ viewport }
        team_cdn={ team_cdn }
        stats={ stats.stats01 }
        info={ stats.info }
    />
  {/if}
</main>

<style></style>
