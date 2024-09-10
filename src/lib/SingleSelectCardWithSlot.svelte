<script>
  import NavBtns from "$lib/NavBtns.svelte";
  export let options = []; // Array of card options
  export let selectedOption = null; // Allow two-way binding for selected option
  export let slotPosition = null; // Position where the content will be shown

  // Function to handle selecting a card
  function selectOption(option, index) {
    selectedOption = option;
    slotPosition = index; // Save the index to show content between cards
  }

  export let nextAction = () => {}; // Function to handle the "Next" button
  export let prevAction = null; // Function to handle the "Previous" button, if provided
</script>

<div class="grid grid-cols-1 gap-2">
  {#each options as option, index}
    <div>
      <!-- Card -->
      <div
        class={`p-3 sm:p-4 md:p-6 relative ring-1 transition-all duration-300 rounded-2xl sm:rounded-2xl ${
          selectedOption === option.title
            ? "bg-white ring-1 ring-orange-500"
            : "bg-white hover:ring-orange-500 ring-slate-300"
        }`}
        on:click={() => selectOption(option.title, index)}
      >
        <div
          class={`sticky top-0 bg-white/90 backdrop-blur-md ${selectedOption === option.title ? "border-b pb-4 border-b-slate-200" : ""}`}
        >
          <div class="flex justify-between gap-2 items-baseline">
            <h3
              class={`font-semibold text-base sm:text-xl text-balance leading-tight ${
                selectedOption === option.title ? "text-orange-600" : ""
              } ${option.description.length > 0 ? "" : ""}`}
            >
              {option.title}
            </h3>
            <p class="font-semibold sm:text-xl text-orange-600 shrink-0">
              {option.price}
            </p>
          </div>
          {#if option.description}
            <p
              class={`text-slate-500 max-w-lg leading-tight text-sm ${
                selectedOption === option.title ? "text-slate-900" : ""
              }`}
            >
              {option.description}
            </p>
          {/if}
        </div>

        <!-- Custom content slot (shown after the selected card) -->
        {#if slotPosition === index}
          <div class="mt-4">
            <slot />
          </div>
        {/if}
        {#if selectedOption === option.title}
          <div class="mt-4">
            <NavBtns {nextAction} {prevAction} />
          </div>
        {/if}
      </div>
    </div>
  {/each}
</div>
