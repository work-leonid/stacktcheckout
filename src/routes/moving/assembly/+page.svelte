<script>
  import Header from "$lib/header.svelte";
  import Footer from "$lib/footer.svelte";

  import HeadlineCard from "$lib/HeadlineCard.svelte";
  import CardWithStepper from "$lib/CardWithStepper.svelte";
  import CardWithContent from "$lib/SingleSelectCardWithSlot.svelte";
  import CustomCard from "$lib/CustomCard.svelte";
  import Stepper from "$lib/Stepper.svelte";
  import { goto } from "$app/navigation";

  let itemCount = 1; // Track the stepper count
  let totalPrice = 0; // Initialize total price
  $: totalPrice = itemCount === 0 ? 0 : 179 + (itemCount - 1) * 42;

  let multiselectedOptions = [];
  let currentPrice = "Total £99";

  function goToNextPage() {
    goto("/moving/storagecollection");
  }
  function goToPreviousPage() {
    goto("/moving/cleaning");
  }

  const assemblyItems = [
    {
      title: "Wardrobe",
      description: "",
      price: "£93",
      image: "assembly/wardrobe.svg",
    },
    {
      title: "Office desk",
      description: "",
      price: "£93",
      image: "assembly/desk.svg",
    },
    {
      title: "Dining table",
      description: "",
      price: "£62",
      image: "assembly/table.svg",
    },
    {
      title: "Single bed",
      description: "",
      price: "£47",
      image: "assembly/bed.svg",
    },
    {
      title: "Double or King bed",
      description: "",
      price: "£77",
      image: "assembly/kingbed.svg",
    },
    {
      title: "TV Stand",
      description: "",
      price: "£69",
      image: "assembly/tvstand.svg",
    },
    {
      title: "Bookcase",
      description: "",
      price: "£85",
      image: "assembly/bookcase.svg",
    },
    {
      title: "Sofa",
      description: "",
      price: "£23",
      image: "assembly/sofa.svg",
    },
  ];

  const assemblyOptions = [
    {
      title: "No, thank you",
      description: "I'll do it myself",
      price: "",
    },
    {
      title: "Assemble/Disassemble by separate furnitures",
      description: "Select only what do you need",
      price: "from £23",
    },
    {
      title: "Assemble/Disassemble with fixed price",
      description: "Only one piece of furniture",
      price: "£41",
    },
  ];
  let packingSelectedOption = "Assemble/Disassemble by separate furnitures";
  let slotPosition = 1;
</script>

<!-- Main layout -->
<div class="flex flex-col gap-8">
  <Header price={currentPrice} />

  <HeadlineCard
    headline="Assembly / Disassembly"
    subheadline="Whether it's furniture, machinery, or electronics, skilled professionals ensure precise assembly or disassembly, guaranteeing seamless functionality or safe removal"
    image="/img/assembly.svg"
    altText="Packing service"
  />

  <CardWithContent
    options={assemblyOptions}
    bind:selectedOption={packingSelectedOption}
    bind:slotPosition
    nextAction={goToNextPage}
    prevAction={goToPreviousPage}
  >
    {#if packingSelectedOption === "Assemble/Disassemble by separate furnitures"}
      <CustomCard
        headline="Professional assembly/disassembly service"
        subheadline="We will carefully assemble or disassemble your furniture or equipment, ensuring that it is done correctly and safely."
        image="/img/packing/bighouse.svg"
        altText="Packing service"
      >
        <CardWithStepper options={assemblyItems} />
      </CustomCard>
    {/if}
  </CardWithContent>

  <Footer />
</div>
