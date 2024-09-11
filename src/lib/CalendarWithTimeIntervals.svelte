<script>
  import TimePill from "$lib/timepill.svelte";
  import Calendar from "$lib/calendar.svelte";
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
    <div class="my-6">
      <div>
        <div class="relative">
          <div>
            <div class="flex gap-1 z-40 isolate">
              <div class="w-2/4 flex flex-col justify-between">
                <span class="leading-tight text-slate-600 text-xs inline-block"
                  >Movers arraiving between 9:00-11:00
                </span>
                <div
                  class="h-2 block bg-gradient-to-l from-orange-600 to-orange-50 rounded-full"
                ></div>
              </div>
              <div class="w-2/4">
                <span
                  class="leading-tight text-center text-slate-600 text-xs inline-block"
                  >Packing, moving, disassembling</span
                >
                <div class="h-2 block bg-orange-600 rounded-full"></div>
              </div>
              <div class="w-1/5 flex flex-col justify-between">
                <span
                  class="leading-tight text-slate-600 text-xs text-right inline-block"
                  >Moving out</span
                >
                <div
                  class="h-2 block bg-gradient-to-r from-orange-600 rounded-full"
                ></div>
              </div>
              <div
                class="bg-slate-100 rounded-full hidden -z-10 h-2 w-full absolute bottom-0"
              ></div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <TimePill />
  </div>
</div>
