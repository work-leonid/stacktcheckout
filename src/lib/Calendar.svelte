<script>
  // Static calendar data
  let month = "September";
  let year = 2024;
  let daysOfWeek = ["Su", "Mo", "Tu", "We", "Th", "Fr", "Sa"];
  let dates = [
    // Empty slots for previous month
    "",
    "",
    "",
    "",
    "",
    "",
    "1",
    "2",
    "3",
    "4",
    "5",
    "6",
    "7",
    "8",
    "9",
    "10",
    "11",
    "12",
    "13",
    "14",
    "15",
    "16",
    "17",
    "18",
    "19",
    "20",
    "21",
    "22",
    "23",
    "24",
    "25",
    "26",
    "27",
    "28",
    "29",
    "30",
    "",
    "",
    "",
    "",
    "",
    "",
  ];
</script>

<div class="flex justify-between max-w-sm items-center mb-4">
  <button class="text-gray-500">
    <svg
      xmlns="http://www.w3.org/2000/svg"
      viewBox="0 0 20 20"
      fill="currentColor"
      class="size-7"
    >
      <path
        fill-rule="evenodd"
        d="M11.78 5.22a.75.75 0 0 1 0 1.06L8.06 10l3.72 3.72a.75.75 0 1 1-1.06 1.06l-4.25-4.25a.75.75 0 0 1 0-1.06l4.25-4.25a.75.75 0 0 1 1.06 0Z"
        clip-rule="evenodd"
      />
    </svg>
  </button>
  <h2 class="font-semibold text-lg">{month} {year}</h2>
  <button class="text-gray-500">
    <svg
      xmlns="http://www.w3.org/2000/svg"
      viewBox="0 0 20 20"
      fill="currentColor"
      class="size-7"
    >
      <path
        fill-rule="evenodd"
        d="M8.22 5.22a.75.75 0 0 1 1.06 0l4.25 4.25a.75.75 0 0 1 0 1.06l-4.25 4.25a.75.75 0 0 1-1.06-1.06L11.94 10 8.22 6.28a.75.75 0 0 1 0-1.06Z"
        clip-rule="evenodd"
      />
    </svg>
  </button>
</div>

<!-- Days of the week -->
<div class="calendar-grid max-w-sm">
  {#each daysOfWeek as day}
    <div class="font-semibold">{day}</div>
  {/each}
</div>

<!-- Calendar dates -->
<div class="calendar-grid max-w-sm">
  {#each dates as date, index}
    <div
      class="{date === '' ? 'inactive' : ''} {date === '9'
        ? 'size-12 border-2 flex items-center justify-center border-slate-900'
        : ''} {date === '11'
        ? 'bg-orange-600 text-white size-12 flex items-center justify-center'
        : ''}"
    >
      {date}
    </div>
  {/each}
</div>

<style>
  /* Customize styling here */
  .calendar-grid {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    gap: 4px;
    text-align: center;
  }

  .calendar-grid div {
    padding: 10px;
    border-radius: 50%;
    font-weight: 500;
  }

  .inactive {
    color: #d3d3d3;
  }

  .active {
    background-color: #f97316;
    color: white;
  }

  .selected {
    border: 2px solid black;
    border-radius: 50%;
  }
</style>
