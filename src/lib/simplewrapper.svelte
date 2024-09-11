<script>
  export let title;
  export let subheadline;
</script>

<div
  class="p-3 border sm:p-4 sm:pt-0 relative cursor-default transition-all duration-300 rounded-2xl sm:rounded-2xl bg-white"
>
  <div
    class="sticky z-40 sm:pt-4 top-0 bg-white/90 backdrop-blur-md border-b pb-4 border-b-slate-200"
  >
    <div class="flex flex-col items-baseline">
      <h3 class="font-semibold text-base sm:text-xl text-balance leading-tight">
        {title}
      </h3>
      {#if subheadline}
        <p>{subheadline}</p>
      {/if}
    </div>
  </div>
  <div class="mt-4">
    <slot />
  </div>
</div>
