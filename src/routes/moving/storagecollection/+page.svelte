<script>
  import Header from "$lib/header.svelte";
  import Footer from "$lib/footer.svelte";

  import HeadlineCard from "$lib/HeadlineCard.svelte";
  import SingleSelectCardWithSlot from "$lib/SingleSelectCardWithSlot.svelte";
  import SingleSelectCardWithoutSlot from "$lib/SingleSelectCardWithoutSlot.svelte";
  import MonthPicker from "$lib/MonthPicker.svelte";
  import { goto } from "$app/navigation";

  let itemCount = 1; // Track the stepper count
  let totalPrice = 0; // Initialize total price
  $: totalPrice = itemCount === 0 ? 0 : 179 + (itemCount - 1) * 42;

  let multiselectedOptions = [];
  let currentPrice = "Total £99";

  function goToNextPage() {
    goto("/moving/calendar");
  }
  function goToPreviousPage() {
    goto("/moving/cleaning");
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
      image: "storage/various.svg",
    },
    {
      title: "Wardrobe",
      description: "5x3x6 ft",
      price: "£19.9/week",
      image: "storage/wardrobe.svg",
    },
    {
      title: "Small room",
      description: "6x4x8 ft",
      price: "£24.9/week",
      image: "storage/smallroom.svg",
    },
    {
      title: "Studio flat",
      description: "6x6x8 ft",
      price: "£27.9/week",
      image: "storage/studio.svg",
    },
    {
      title: "Half of a Garage",
      description: "8x6x8 ft",
      price: "£31.9/week",
      image: "storage/halfofagarage.svg",
    },
    {
      title: "Small Office",
      description: "9x8x8 ft",
      price: "£45.9/week",
      image: "storage/smalloffice.svg",
    },
    {
      title: "1-Car Garage",
      description: "12x8x8 ft",
      price: "£59.9/week",
      image: "storage/cargarage.svg",
    },
    {
      title: "House+",
      description: "Price per 1 sqft",
      price: "£0.82/week",
      image: "storage/house.svg",
    },
  ];

  const packingOptions = [
    {
      title: "No, thank you",
      description: "I don't need storage",
      price: "",
    },

    {
      title: "Storage collection",
      description:
        "You can store as many of your belongings as you like in our secure storage spaces",
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
  <Header />

  <HeadlineCard
    headline="Storage collection"
    subheadline="Need to store items while moving? We got you covered."
    image="/img/packing/bighouse.svg"
    altText="Packing service"
  />

  <SingleSelectCardWithSlot
    options={packingOptions}
    bind:selectedOption={packingSelectedOption}
    bind:slotPosition
    nextAction={goToNextPage}
    prevAction={goToPreviousPage}
  >
    {#if packingSelectedOption === "Storage collection"}
      <div class="flex flex-col mt-4 gap-2">
        <h2 class="text-lg font-semibold leading-tight">
          The longer you store, the more you save
        </h2>
        <MonthPicker options={dateOptions} />
      </div>
      <div class="flex flex-col mt-4 gap-2">
        <h3 class="text-lg font-semibold leading-tight">
          How much space do you need?
        </h3>
        <SingleSelectCardWithoutSlot
          options={storagePlaces}
          bind:monthSelectedOption
        />
      </div>
    {/if}
  </SingleSelectCardWithSlot>

  <Footer price={currentPrice} />
</div>
