<script>
  import Header from "$lib/header.svelte";
  import Footer from "$lib/footer.svelte";
  import { goto } from "$app/navigation";

  import HeadlineCard from "$lib/HeadlineCard.svelte";
  import MultiSelectCard from "$lib/MultiSelectCard.svelte";
  import SingleSelectCardWithSlot from "$lib/SingleSelectCardWithSlot.svelte";
  import ImageDescription from "$lib/ImageDescription.svelte";

  let multiselectedOptions = []; // Track the selected options (multi-select)
  let currentPrice = "Moving total £169";

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
  let benefitsMiniMove = [
    "up to 2 hrs",
    "max 10 boxes or similar sized items",
    "up to 25 miles",
    "2 movers",
    "1 van",
  ];
  let benefits1Bedroom = [
    "1 van",
    "2 movers",
    "max 30 large boxes",
    "up to 25 miles",
  ];
  let benefits2Bedrooms = [
    "1 van",
    "3 movers",
    "max 55 large boxes",
    "up to 25 miles",
  ];
  let benefits3Bedrooms = [
    "2 vans",
    "4 movers",
    "max 75 large boxes",
    "up to 25 miles",
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

  <SingleSelectCardWithSlot
    nextAction={goToNextPage}
    options={flatOptions}
    bind:selectedOption
    bind:slotPosition
  >
    {#if selectedOption === "Mini Move"}
      <ImageDescription
        title="The most cost-effective small space moving option not only among other options, but also among competitors."
        image="/img/moving/mini.svg"
        benefits={benefitsMiniMove}
      />
    {/if}
    {#if selectedOption === "1 bedroom/Studio"}
      <ImageDescription
        title="Our team makes your small move stress-free! Whether it’s a compact
        space or a cozy home, we handle every detail with care, ensuring your
        belongings arrive safely at your new place. Quick, efficient, and
        affordable moving services!"
        image="/img/moving/1bed.svg"
        benefits={benefits1Bedroom}
      />
    {/if}
    {#if selectedOption === "2 bedrooms"}
      <ImageDescription
        title="Our professional movers are ready to take the hassle out of your move.
        From packing and loading to transporting and unloading, we provide
        full-service moving tailored to your needs. Trust us to make your move
        smooth and seamless!"
        image="/img/moving/2bed.svg"
        benefits={benefits2Bedrooms}
      />
    {/if}
    {#if selectedOption === "3 bedrooms"}
      <ImageDescription
        title="Our experienced movers ensure every room is packed, transported, and
        unpacked with precision and care. We handle large moves with ease, so
        you can focus on settling into your new home. Reliable, professional,
        and efficient service!"
        image="/img/moving/3bed.svg"
        benefits={benefits3Bedrooms}
      />
    {/if}

    {#if selectedOption === "Personalised quote"}
      <p class="mb-4 leading-tight">
        We’re here to help! Contact us for a personalised quote tailored to your
        move. Whether it’s a unique request or a custom plan, we’ll ensure you
        get the best service at the right price. Get in touch today for your
        bespoke moving solution!
      </p>
      <MultiSelectCard options={multiselectOptions} bind:multiselectedOptions />
    {/if}
  </SingleSelectCardWithSlot>

  <Footer price={currentPrice} />
</div>
