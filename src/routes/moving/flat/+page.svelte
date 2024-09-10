<script>
  import Header from "$lib/header.svelte";
  import Footer from "$lib/footer.svelte";
  import { goto } from "$app/navigation";

  import HeadlineCard from "$lib/HeadlineCard.svelte";
  import MultiSelectCard from "$lib/MultiSelectCard.svelte";
  import CardWithContent from "$lib/SingleSelectCardWithSlot.svelte";
  import CustomCard from "$lib/CustomCard.svelte";
  import CalendarWithTimeIntervals from "$lib/CalendarWithTimeIntervals.svelte";

  let multiselectedOptions = []; // Track the selected options (multi-select)
  let currentPrice = "Total £99";

  // Function to handle card selection and navigate to packing page if selected
  function goToNextPage() {
    goto("/moving/packing");
  }
  const benefits = [
    "No overtime charges",
    "Professional movers with bodycams",
    "Insurance included in price",
  ];

  const multiselectOptions = [
    {
      title: "Moving",
      description: "",
      price: "from £999",
    },
    {
      title: "Packing",
      description: "",
      price: "from £99",
    },
    { title: "Cleaning", description: "", price: "£209" },
    { title: "Assembly/Disassembly", description: "", price: "£49" },
  ];

  const flatOptions = [
    {
      title: "Mini Move",
      description:
        "up to 2 hrs • max 10 boxes or similar sized items • up to 25 miles",
      price: "£169",
    },
    {
      title: "1 bedroom/Studio",
      description: "max 30 large boxes • up to 25 miles",
      price: "£259",
    },
    {
      title: "2 bedrooms",
      description: "max 55 large boxes • up to 25 miles",
      price: "£449",
    },
    {
      title: "3 bedrooms",
      description: "max 75 large boxes • up to 25 miles",
      price: "£849",
    },
    {
      title: "Personalised quote",
      description:
        "If you have a specific need, we can create a personalised quote for you",
      price: "from £99",
    },
  ];
  let selectedOption = "Mini Move"; // Preselect the "Mini Move" option
  let slotPosition = 0;
</script>

<div class="flex flex-col gap-8">
  <Header price={currentPrice} />
  <HeadlineCard
    {benefits}
    headline="Moving - flexible & adaptive to your needs"
    subheadline=""
    image="/img/moving.svg"
  />

  <CardWithContent
    nextAction={goToNextPage}
    options={flatOptions}
    bind:selectedOption
    bind:slotPosition
  >
    {#if selectedOption === "Mini Move"}
      <div class="mt-4">
        <CalendarWithTimeIntervals />
      </div>
    {/if}

    {#if selectedOption === "1 bedroom/Studio"}
      <div class="mt-4">
        <CalendarWithTimeIntervals />
      </div>
    {/if}

    {#if selectedOption === "2 bedrooms"}
      <div class="mt-4">
        <CalendarWithTimeIntervals />
      </div>
    {/if}

    {#if selectedOption === "3 bedrooms"}
      <div class="mt-4">
        <CalendarWithTimeIntervals />
      </div>
    {/if}

    {#if selectedOption === "Personalised quote"}
      <CustomCard
        headline="Need something special?"
        subheadline="Select your needs and we'll call you back to arrange your moving and
                    other services"
        image="/img/packing/bighouse.svg"
        altText="Packing service"
      >
        <MultiSelectCard
          options={multiselectOptions}
          bind:multiselectedOptions
        />
      </CustomCard>
      <div class="mt-4">
        <CalendarWithTimeIntervals />
      </div>
    {/if}
  </CardWithContent>

  <Footer price={currentPrice} />
</div>
