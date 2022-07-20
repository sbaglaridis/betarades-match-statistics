<script>
  import env from "../env.js";

  let stats = null
  let viewport = 'mobile';

  (function checkViewport () {
      if (window.innerWidth >= 992) {
        viewport = 'desktop'
      } else if (window.innerWidth >= 576) {
        viewport = 'tablet'
      } else {
        viewport = 'mobile'
      }

    window.addEventListener('resize', checkViewport);
  })();

  const matchStatistics = document.getElementById('match-statistics')
  const url = matchStatistics.getAttribute('data-url')

  fetch(`${env.BASE_URL}/${url}`)
    .then(response => response.json())
    .then(data => stats = data)
    .catch(error => stats = {})
    .finally(() => {
      const blockLoader = matchStatistics.querySelector('#match-statistics-loader')

      blockLoader && blockLoader.remove()
    })

  const stats_list = {
    'stats01': { show: true, label: 'Στατιστικά' },
    'stats02': { show: true, label: 'ΤΕΛΕΥΤΑΙΟΙ ΑΓΩΝΕΣ' },
    'stats03': { show: true, label: 'OVER/UNDER' },
    'stats04': { show: true, label: 'ΓΚΟΛ & ΗΜΙΧΡΟΝΑ' },
    'stats05': { show: true, label: 'ΗΜΙΧΡΟΝΑ/ΤΕΛΙΚΑ' },
    'stats06': { show: true, label: 'ΓΚΟΛ ΑΝΑ ΛΕΠΤΟ' },
    'stats07': { show: true, label: 'ΣΚΟΡΕΡΣ' },
    'stats08': { show: true, label: 'ΤΑ ΣΕΡΙ' },
    'stats09': { show: true, label: 'ΒΑΘΜΟΛΟΓΙΑ Α\' Νορβηγίας' },
    'stats10': { show: true, label: 'ΕΠΟΜΕΝΟΙ ΑΓΩΝΕΣ ' },
  }

  $: console.log('viewport is:', viewport)
  $: console.log('data:', stats)
</script>

{#if stats && stats.info }
    {#each Object.keys(stats_list) as key}
        {#if stats_list[key].show && stats[key]}
            {#await import(`./components/${key}.svelte`) then component}
                <svelte:component
                    this={ component.default }
                    label={ stats_list[key].label }
                    info={ stats.info }
                    stats={ stats[key.toLowerCase()] }
                    viewport={ viewport }
                    key={ key }
                />
            {/await}
        {/if}
    {/each}
{/if}
