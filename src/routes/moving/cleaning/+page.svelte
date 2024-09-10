<script>
  import Header from "$lib/Header.svelte";
  import Footer from "$lib/Footer.svelte";

  import TimePill from "$lib/TimePill.svelte";
  import HeadlineCard from "$lib/HeadlineCard.svelte";
  import CardWithStepper from "$lib/CardWithStepper.svelte";
  import CardWithContent from "$lib/SingleSelectCardWithSlot.svelte";
  import MultiSelectCard from "$lib/MultiSelectCard.svelte";
  import CustomCard from "$lib/CustomCard.svelte";
  import Calendar from "$lib/Calendar.svelte";

  import { goto } from "$app/navigation";

  let itemCount = 1; // Track the stepper count
  let totalPrice = 0; // Initialize total price
  $: totalPrice = itemCount === 0 ? 0 : 179 + (itemCount - 1) * 42;

  let multiselectedOptions = [];
  let currentPrice = "Total £99";

  function goToNextPage() {
    goto("/moving/assembly");
  }
  function goToPreviousPage() {
    goto("/moving/packing");
  }

  const packingMeterials = [
    {
      title: "Small boxes",
      description: "36cm x 36cm x36cm -14inch (up to 15kg)",
      price: "£2.72/box",
    },
    {
      title: "Large boxes",
      description: "46 × 46 × 46cm -18 inches (up to 20kg)",
      price: "£2.72/box",
    },
    {
      title: "Wardrobe boxes",
      description: "holds 20-30 hangers",
      price: "£8.1/box",
    },
    {
      title: "Tape",
      description: "Brown PVC tape: 5cm x 6600cm",
      price: "£2.72/tape",
    },
    {
      title: "Bubble wrap(s)",
      description: "30cm x 50m roll",
      price: "£40/roll",
    },
    {
      title: "Paper pack",
      description: "White packing paper pack",
      price: "£11/box",
    },
  ];

  const cleaningOptions = [
    {
      title: "No, thank you",
      description: "I'll pack all my items myself",
      price: "",
    },

    {
      title: "I need a cleaning service",
      description: "2 cleaners • 72h guarantee",
      price: "£229",
    },
  ];
  let cleaningSelectedOption = "I need a cleaning service";
  let slotPosition = 1;

  let allCleaningOptions = ["Kitchen", "Bathrooms", "Bedrooms", "Common areas"];
</script>

<!-- Main layout -->
<div class="flex flex-col gap-8">
  <Header price={currentPrice} />

  <HeadlineCard
    headline="Professional End-of-Tenancy Cleaning"
    subheadline="From top to bottom, we’ll clean and sanitise your kitchen, bathrooms, bedrooms and common areas."
    image="/img/cleaning.svg"
    altText="Stackt"
  />

  <CardWithContent
    options={cleaningOptions}
    bind:selectedOption={cleaningSelectedOption}
    bind:slotPosition
    nextAction={goToNextPage}
    prevAction={goToPreviousPage}
  >
    {#if cleaningSelectedOption === "All-inclusive packing"}
      <CustomCard
        headline="Professional packing with all-inclusive materials"
        subheadline="We will carefully pack all your items in one go in the safest way possible. You'll get unlimited packing materials included."
        image="/img/packing/bighouse.svg"
        altText="Packing service"
      >
        <div class="flex gap-1 flex-wrap">
          {#each allCleaningOptions as option}
            <span
              class="flex bg-slate-100 ring-1 ring-slate-200 w-fit pl-1 pr-2 py-0.5 rounded-full text-sm gap-0.5 text-slate-800 items-center"
              ><svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 20 20"
                fill="currentColor"
                class="size-4 text-orange-600"
              >
                <path
                  fill-rule="evenodd"
                  d="M10 18a8 8 0 1 0 0-16 8 8 0 0 0 0 16Zm3.857-9.809a.75.75 0 0 0-1.214-.882l-3.483 4.79-1.88-1.88a.75.75 0 1 0-1.06 1.061l2.5 2.5a.75.75 0 0 0 1.137-.089l4-5.5Z"
                  clip-rule="evenodd"
                />
              </svg>
              {option}</span
            >
          {/each}
        </div>
      </CustomCard>
    {/if}

    {#if cleaningSelectedOption === "I need a cleaning service"}
      <CustomCard
        headline="From top to bottom, we’ll clean everywhere"
        subheadline="All our standard cleanings include dusting and washing of all reachable surfaces, wiping the outside of kitchen appliances & cabinets, basic cleaning of the bathrooms, and vacuuming & mopping of all floors"
        image="/img/cleaning-card.svg"
        altText="Packing service"
      >
        <div class="flex gap-1 flex-wrap">
          {#each allCleaningOptions as option}
            <span
              class="flex bg-slate-100 ring-1 ring-slate-200 w-fit pl-1 pr-2 py-0.5 rounded-full text-sm gap-0.5 text-slate-800 items-center"
              ><svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 20 20"
                fill="currentColor"
                class="size-4 text-orange-600"
              >
                <path
                  fill-rule="evenodd"
                  d="M10 18a8 8 0 1 0 0-16 8 8 0 0 0 0 16Zm3.857-9.809a.75.75 0 0 0-1.214-.882l-3.483 4.79-1.88-1.88a.75.75 0 1 0-1.06 1.061l2.5 2.5a.75.75 0 0 0 1.137-.089l4-5.5Z"
                  clip-rule="evenodd"
                />
              </svg>
              {option}</span
            >
          {/each}
        </div>
      </CustomCard>
      <div class="flex flex-col mt-4 gap-4">
        <div>
          <h3 class="text-lg sm:text-xl mb-4 leading-tight font-semibold">
            Cleaning on <span
              class="font-semibold leading-tight text-xl text-orange-600"
            >
              Saturday, September 14
            </span>
          </h3>
          <div class="*:mx-auto">
            <Calendar />
          </div>
        </div>
        <div>
          <h3 class="text-lg sm:text-xl text-balance mb-4 font-semibold">
            Estimated time of arrival of the cleaners <span
              class="text-orange-600">between 9:00-15:00</span
            >
          </h3>
          <TimePill withTabs={false} />
        </div>
      </div>
    {/if}
  </CardWithContent>

  <Footer />
</div>
