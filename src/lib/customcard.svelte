<script>
  export let headline = ""; // Optional headline
  export let subheadline = ""; // Optional subheadline
  export let image = ""; // Optional image source
  export let altText = ""; // Optional image alt text
</script>

<div class="flex mt-4 gap-4 flex-col">
  <div>
    {#if headline}
      <h3 class="text-base sm:text-xl leading-tight font-semibold">
        {headline}
      </h3>
    {/if}

    {#if subheadline}
      <p class="text-sm leading-snug">{subheadline}</p>
    {/if}
  </div>

  <!-- Slot for additional content passed from the parent component -->
  <slot />
</div>
