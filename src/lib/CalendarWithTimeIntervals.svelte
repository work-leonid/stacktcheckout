<script>
  import TimePill from "$lib/TimePill.svelte";
  import Calendar from "$lib/Calendar.svelte";
</script>

<div class="flex flex-col gap-4">
  <div>
    <h3 class="text-lg sm:text-xl leading-tight font-semibold">
      Moving date <span
        class="font-semibold leading-tight mb-2 text-orange-600"
      >
        Saturday, September 14
      </span>
    </h3>
  </div>
  <div class="mx-auto">
    <Calendar />
  </div>

  <div>
    <h3 class="text-lg sm:text-xl mb-2 leading-tight font-semibold">
      Estimated time of arrival of the movers <span class="text-orange-600"
        >between 9:00-11:00.
      </span> Don't forget that the movers need more time to pack up and move things
      out.
    </h3>
    <TimePill />
  </div>
</div>
