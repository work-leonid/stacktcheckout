<script>
  import Header from "$lib/Header.svelte";
  import Footer from "$lib/Footer.svelte";

  import HeadlineCard from "$lib/HeadlineCard.svelte";
  import CardWithStepper from "$lib/CardWithStepper.svelte";
  import CardWithContent from "$lib/SingleSelectCardWithSlot.svelte";
  import CustomCard from "$lib/CustomCard.svelte";
  import SingleSelectCardWithoutSlot from "$lib/SingleSelectCardWithoutSlot.svelte";
  import MonthPicker from "$lib/MonthPicker.svelte";
  import { goto } from "$app/navigation";

  let itemCount = 1; // Track the stepper count
  let totalPrice = 0; // Initialize total price
  $: totalPrice = itemCount === 0 ? 0 : 179 + (itemCount - 1) * 42;

  let multiselectedOptions = [];
  let currentPrice = "Total £99";

  function goToNextPage() {
    goto("/moving/cleaning");
  }
  function goToPreviousPage() {
    goto("/moving/flat");
  }

  const additionalServices = [
    {
      title: "Storage collection",
      description:
        "Get rid of unwanted items! The longer you store, the more you save.",
      price: "£169",
    },
  ];
  const storagePlaces = [
    {
      title: "Various items",
      description: "3x3x8 ft",
      price: "£11.9/week",
    },
    {
      title: "Wardrobe",
      description: "5x3x6 ft",
      price: "£19.9/week",
    },
    {
      title: "Small room",
      description: "6x4x8 ft",
      price: "£24.9/week",
    },
    {
      title: "Studio flat",
      description: "6x6x8 ft",
      price: "£27.9/week",
    },
    {
      title: "Half of a Garage",
      description: "8x6x8 ft",
      price: "£31.9/week",
    },
    {
      title: "Small Office",
      description: "9x8x8 ft",
      price: "£45.9/week",
    },
    {
      title: "1-Car Garage",
      description: "12x8x8 ft",
      price: "£59.9/week",
    },
    {
      title: "House+",
      description: "Price per 1 sqft",
      price: "£0.82/week",
    },
  ];

  const packingOptions = [
    {
      title: "No, thank you",
      description: "I'll pack all my items myself",
      price: "",
    },

    {
      title: "Storage collection",
      description: "Get rid of unwanted items",
      price: "from £9",
    },
  ];

  let dateOptions = [
    {
      title: "Monthly",
      badge: "",
    },
    {
      title: "3 months",
      badge: "-25%",
    },
    {
      title: "6 months",
      badge: "-40%",
    },
  ];
  let packingSelectedOption = "Storage collection";
  let slotPosition = 1;

  let monthSelectedOption = "3 months";
</script>

<!-- Main layout -->
<div class="flex flex-col gap-8">
  <Header price={currentPrice} />

  <HeadlineCard
    headline="Storage collection"
    subheadline="The longer you store, the more you save."
    image="/img/packing/bighouse.svg"
    altText="Packing service"
  />

  <CardWithContent
    options={packingOptions}
    bind:selectedOption={packingSelectedOption}
    bind:slotPosition
  >
    {#if packingSelectedOption === "Storage collection"}
      <CustomCard
        headline="The longer you store, the more you save"
        subheadline=""
        image="/img/packing/bighouse.svg"
        altText="Packing service"
      >
        <MonthPicker options={dateOptions} />
      </CustomCard>
    {/if}
  </CardWithContent>

  {#if packingSelectedOption === "Storage collection"}
    <div class="flex flex-col gap-2">
      <h3 class="text-xl font-semibold">How much space do you need?</h3>
      <SingleSelectCardWithoutSlot
        options={storagePlaces}
        bind:monthSelectedOption
      />
    </div>
  {/if}

  <Footer nextAction={goToNextPage} prevAction={goToPreviousPage} />
</div>
