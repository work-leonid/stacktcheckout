<script>
  export let options = [];
  export let selectedOption = null; // Bind a single selected option

  // Handle single option selection
  function selectOption(option) {
    selectedOption = option.title;
  }
</script>

<div class="grid sm:grid-cols-2 gap-2">
  {#each options as option}
    <div
      class={`p-3 md:p-4 border group cursor-pointer transition-all duration-300 rounded-2xl ${
        selectedOption === option.title
          ? "bg-orange-50 border-orange-500 ring-4 ring-orange-500/20"
          : "bg-white  border-slate-300 hover:border-orange-500 ring-0"
      }`}
      on:click={() => selectOption(option)}
    >
      <div class="flex flex-col justify-between">
        {#if option.image}
          <img
            src={`/img/${option.image}`}
            alt="Wardrobe"
            class="size-20 group-hover:scale-105 transition-all duration-300 sm:mb-2 sm:w-full sm:h-auto"
          />
        {/if}

        <div class="flex flex-col flex-1">
          <div class="flex justify-between items-baseline">
            <h3
              class={`font-semibold leading-tight ${
                selectedOption === option.title ? "text-orange-600" : ""
              }`}
            >
              {option.title}
            </h3>
            {#if option.price}
              <p class="font-semibold text-orange-600 shrink-0">
                {option.price}
              </p>
            {/if}
          </div>
          {#if option.description && option.description.trim() !== ""}
            <p
              class={`text-slate-500 leading-tight text-xs ${
                selectedOption === option.title ? "text-slate-900" : ""
              }`}
            >
              {option.description}
            </p>
          {/if}
        </div>
      </div>
    </div>
  {/each}
</div>
