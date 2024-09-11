<script>
  export let price = "Moving total £169"; // Default price, can be updated per page
  let benefits = [
    "Insurance included in price",
    "Free 24h cancellation",
    "No overtime charges",
  ];
</script>

<!-- Footer text with icons -->
<div class="p-4 flex flex-col bg-white ring-1 ring-slate-200 rounded-2xl">
  <div class="flex text-xl gap-2 items-center mb-2 font-semibold">
    {price}
  </div>

  <div class="flex-wrap flex gap-y-3 gap-x-3">
    {#each benefits as benefit}
      <span class="flex items-center gap-1 leading-tight">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 16 16"
          fill="currentColor"
          class="size-5 text-orange-600"
        >
          <path
            fill-rule="evenodd"
            d="M12.416 3.376a.75.75 0 0 1 .208 1.04l-5 7.5a.75.75 0 0 1-1.154.114l-3-3a.75.75 0 0 1 1.06-1.06l2.353 2.353 4.493-6.74a.75.75 0 0 1 1.04-.207Z"
            clip-rule="evenodd"
          />
        </svg>
        {benefit}
      </span>
    {/each}
    <div
      class="flex px-2 py-6 bg-orange-50 w-full text-center justify-center rounded-xl items-center gap-1"
    >
      <div>
        <p class="font-semibold">5% OFF for All-Inclusive package!</p>
        Order Moving+Packing+Cleaning and get 5% OFF. Promo code:
        <span class="font-semibold text-orange-600">STACKT</span>
      </div>
    </div>
  </div>
</div>
