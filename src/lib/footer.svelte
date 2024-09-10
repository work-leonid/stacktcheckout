<script>
  export let price = "Total £0"; // Default price, can be updated per page
</script>

<!-- Footer text with icons -->
<div>
  <div class="flex text-xl gap-2 items-center mb-2 font-semibold">
    {price}
  </div>

  <div class="flex-col flex gap-2 justify-center">
    <span class="flex items-center gap-1 leading-tight text-balance">
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
      Insurance included in price
    </span>
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
      Free 24h cancellation
    </span>
    <div
      class="flex p-4 bg-orange-100 rounded-xl items-center gap-1 leading-tight"
    >
      <p>
        <span class="font-semibold"
          >5% OFF for All-Inclusive package!
        </span>Order Moving+Packing+Cleaning and get 5% OFF. Promo code:
        <span class="font-semibold text-orange-600">STACKT</span>
      </p>
    </div>
  </div>
</div>
