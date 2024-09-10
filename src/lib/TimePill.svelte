<script>
  // Time data for 6-hour and 2-hour slots
  let time6hrs = ["9:00 - 15:00", "12:00 - 18:00", "17:00 - 23:00"];
  let time2hrs = [
    "9:00 - 11:00",
    "10:00 - 12:00",
    "12:00 - 14:00",
    "13:00 - 15:00",
    "14:00 - 16:00",
    "17:00 - 19:00",
    "18:00 - 20:00",
    "19:00 - 21:00",
  ];

  // Prop to control whether tabs are shown or not
  export let withTabs = true; // Default: show tabs

  let activeTab = "2hrs"; // Default tab is 2-hour intervals
  let selectedOption = null; // Track the selected time slot

  // Handle single option selection
  function selectOption(option) {
    selectedOption = option.time;
  }

  // Determine which options to show based on the active tab
  $: options =
    activeTab === "2hrs"
      ? time2hrs.map((time) => ({ time }))
      : time6hrs.map((time) => ({ time }));
</script>

<!-- Conditionally show tabs if withTabs is true -->
{#if withTabs}
  <div
    class="flex *:flex-1 p-1 items-center bg-slate-100 rounded-full justify-center gap-1 mb-2"
  >
    <button
      class={`px-4 py-1 font-semibold ${
        activeTab === "2hrs" ? "bg-white" : ""
      } rounded-full transition-all`}
      on:click={() => (activeTab = "2hrs")}
    >
      2hrs
    </button>
    <button
      class={`px-4 py-1 flex gap-3 items-center justify-center font-semibold ${
        activeTab === "6hrs" ? "bg-white" : ""
      } rounded-full transition-all`}
      on:click={() => (activeTab = "6hrs")}
    >
      6hrs
      <span
        class="text-xs leading-none bg-orange-600 px-1.5 py-1 rounded-full text-white"
        >+15%</span
      >
    </button>
  </div>
{/if}

<!-- Time selection grid -->
<div class="grid grid-cols-2 gap-1 text-center">
  {#each options as option}
    <div
      class={`p-3 border cursor-pointer transition-all duration-300 rounded-xl ${
        selectedOption === option.time
          ? "bg-orange-50 border-orange-500"
          : "bg-white border-slate-200"
      }`}
      on:click={() => selectOption(option)}
    >
      <div class="flex flex-col justify-between">
        <h3
          class={`font-semibold leading-tight ${
            selectedOption === option.time ? "text-orange-600" : ""
          }`}
        >
          {option.time}
        </h3>
      </div>
    </div>
  {/each}
</div>
