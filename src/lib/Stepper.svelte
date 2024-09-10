<script>
  export let count = 0; // The current count, initialized to 0
  export let min = 0; // Minimum value (default is 0)
  export let max = Infinity; // Maximum value (default is no limit)

  function increment() {
    if (count < max) {
      count += 1;
    }
  }

  function decrement() {
    if (count > min) {
      count -= 1;
    }
  }
</script>

<div class="flex max-w-64 items-center gap-1">
  <button
    on:click={decrement}
    class="px-5 py-2 inline-flex items-center disabled:bg-slate-50 disabled:text-slate-300 active:scale-90 active:inner-shadow disabled:cursor-not-allowed rounded-full bg-orange-200/70 text-orange-600 hover:bg-orange-200 transition-all duration-300"
    disabled={count <= min}
  >
    <svg
      xmlns="http://www.w3.org/2000/svg"
      viewBox="0 0 16 16"
      fill="currentColor"
      class="size-5"
    >
      <path d="M3.75 7.25a.75.75 0 0 0 0 1.5h8.5a.75.75 0 0 0 0-1.5h-8.5Z" />
    </svg>
  </button>

  <span
    class="font-semibold bg-white py-1 rounded-full proportional-nums min-w-16 sm:min-w-24 text-center ring-1 ring-slate-200 text-lg"
    >{count}</span
  >

  <button
    on:click={increment}
    class="px-5 py-2 inline-flex items-center disabled:bg-slate-50 disabled:text-slate-300 active:scale-90 active:inner-shadow disabled:cursor-not-allowed rounded-full bg-orange-200/70 text-orange-600 hover:bg-orange-200 transition-all duration-300"
    disabled={count >= max}
  >
    <svg
      xmlns="http://www.w3.org/2000/svg"
      viewBox="0 0 16 16"
      fill="currentColor"
      class="size-5"
    >
      <path
        d="M8.75 3.75a.75.75 0 0 0-1.5 0v3.5h-3.5a.75.75 0 0 0 0 1.5h3.5v3.5a.75.75 0 0 0 1.5 0v-3.5h3.5a.75.75 0 0 0 0-1.5h-3.5v-3.5Z"
      />
    </svg>
  </button>
</div>
