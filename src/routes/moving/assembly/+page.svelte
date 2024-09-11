<script>
  import Header from "$lib/header.svelte";
  import Footer from "$lib/footer.svelte";

  import HeadlineCard from "$lib/headlinecard.svelte";
  import CardWithStepper from "$lib/cardwithstepper.svelte";
  import CardWithContent from "$lib/singleselectcardwithslot.svelte";
  import ImageDescription from "$lib/imagedescription.svelte";
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
      title: "Assemble/Disassemble by separate furniture",
      description: "Select only what do you need",
      price: "from £23",
    },
    {
      title: "Assemble/Disassemble with fixed price",
      description: "Include 3 wardrobes, 3 beds, 1 desk",
      price: "£549",
    },
  ];
  let fixedPriceBenefits = ["3 wardrobes", "3 beds", "1 desk"];
  let packingSelectedOption = "Assemble/Disassemble by separate furniture";
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
    {#if packingSelectedOption === "Assemble/Disassemble by separate furniture"}
      <div class="flex flex-col gap-4">
        <ImageDescription
          title="We will carefully assemble or disassemble your furniture or equipment, ensuring that it is done correctly and safely."
          image="https://plus.unsplash.com/premium_photo-1661292184470-5ae807de40f5?w=900&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1yZWxhdGVkfDF8fHxlbnwwfHx8fHw%3D"
        />
        <CardWithStepper options={assemblyItems} />
      </div>
    {/if}
    {#if packingSelectedOption === "Assemble/Disassemble with fixed price"}
      <div class="flex flex-col gap-4">
        <ImageDescription
          title="We will carefully assemble or disassemble your furniture or equipment, ensuring that it is done correctly and safely."
          image="https://plus.unsplash.com/premium_photo-1664303777059-cab540d722dd?q=80&w=2670&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
          benefits={fixedPriceBenefits}
        />
      </div>
    {/if}
  </CardWithContent>

  <Footer />
</div>
