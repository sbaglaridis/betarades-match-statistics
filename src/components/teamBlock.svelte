<script>
  export let src;
  export let label;
</script>

<div class="preview-stats__info stats-top-header-bordered g-16 mb-2">
    <div class="preview-stats__team-t-short">
        <img
            src="{ src }"
            alt="{ label }"
            width="28"
            height="28"
            loading="lazy"
        >
    </div>
    <div>{ label }</div>
</div>

