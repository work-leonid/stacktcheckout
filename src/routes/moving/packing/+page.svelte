<script>
  import Header from "$lib/header.svelte";
  import Footer from "$lib/footer.svelte";

  import ImageDescription from "$lib/imagedescription.svelte";
  import HeadlineCard from "$lib/HeadlineCard.svelte";
  import CardWithContent from "$lib/singleselectcardwithslot.svelte";
  import PackingAdditionalServices from "$lib/packingadditional.svelte";
  import Stepper from "$lib/stepper.svelte";
  import { goto } from "$app/navigation";

  let itemCount = 1; // Track the stepper count
  let totalPrice = 0; // Initialize total price
  $: totalPrice = itemCount === 0 ? 0 : 179 + (itemCount - 1) * 42;

  let currentPrice = "Total: one-time £99, per week £19.9";

  function goToNextPage() {
    goto("/moving/cleaning");
  }
  function goToPreviousPage() {
    goto("/moving/flat");
  }

  const benefits = [
    "Proffessional packing materials",
    "Save your time and money",
  ];

  const packingOptions = [
    {
      title: "No, thank you",
      description:
        "I'll pack all my items myself and i don't need any additional packing materials.",
      price: "",
    },

    {
      title: "All-inclusive packing",
      description: "Unlimited packing materials included",
      price: "£349",
    },
    {
      title: "Professional packing service",
      description:
        "We will pack your items in the safest way possible. You can add any additional packing materials if you'd like",
      price: "£259",
    },
    {
      title: "Packing by furniture",
      description:
        "For big furniture like wardrobe, desk, etc. Includes packing materials",
      price: "from £179",
    },
    {
      title: "Additional services",
      description:
        "If you want to pack your own belongings and need professional packing materials.",
      price: "",
    },
  ];
  let packingSelectedOption = "All-inclusive packing";
  let slotPosition = 1;

  let allInclusiveOptions = [
    "Boxes",
    "Paper packs",
    "PVC tape",
    "Bubble wraps",
    "Packing services",
  ];
</script>

<div class="flex flex-col gap-4">
  <Header price={currentPrice} />

  <HeadlineCard
    headline="Pack your items carefully"
    subheadline="Professional packing service for your items"
    image="/img/packing.svg"
    altText="Packing service"
    {benefits}
  />

  <CardWithContent
    options={packingOptions}
    bind:selectedOption={packingSelectedOption}
    bind:slotPosition
    nextAction={goToNextPage}
    prevAction={goToPreviousPage}
  >
    {#if packingSelectedOption === "No, thank you"}
      <PackingAdditionalServices />
    {/if}

    {#if packingSelectedOption === "All-inclusive packing"}
      <div class="flex flex-col gap-8">
        <ImageDescription
          title="We will carefully pack all your items in one go in the safest way possible. You'll get unlimited packing materials included."
          image="https://plus.unsplash.com/premium_photo-1664300914931-76c0f99a96b8?w=900&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NTl8fHBhY2tpbmclMjBib3glMjBtb3ZlcnxlbnwwfDB8MHx8fDE%3D"
          benefits={allInclusiveOptions}
        />
        <PackingAdditionalServices />
      </div>
    {/if}

    {#if packingSelectedOption === "Professional packing service"}
      <div class="flex flex-col gap-8">
        <ImageDescription
          title="We'll use professional packing materials to pack your furniture in the
                  safest way possible. All materials are 100% organic and sustainable.
                  Save your time."
          image="https://plus.unsplash.com/premium_photo-1665203545714-44b60e4c9688?w=900&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NjB8fHBhY2tpbmclMjBib3glMjBtb3ZlcnxlbnwwfDB8MHx8fDE%3D"
        />
        <PackingAdditionalServices />
      </div>
    {/if}

    {#if packingSelectedOption === "Packing by furniture"}
      <div class="flex flex-col gap-8">
        <ImageDescription
          title=""
          image="https://plus.unsplash.com/premium_photo-1723701918806-bf9b3b37a02a?q=80&w=3496&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
        >
          <div class="flex flex-col gap-2">
            <h3 class="text-lg font-semibold leading-tight">
              How many furniture items do you need to pack?
            </h3>
            <Stepper bind:count={itemCount} min={1} />
            <div>
              <p class="text-xl font-semibold">
                Total: <span class="text-orange-600">£{totalPrice}</span>
              </p>
              <p class="text-sm">
                Price includes high quality packing materials and proffesional
                packing service. Only for big furniture.
              </p>
            </div>
          </div>
        </ImageDescription>
        <PackingAdditionalServices />
      </div>
    {/if}
    {#if packingSelectedOption === "Additional services"}
      <PackingAdditionalServices />
    {/if}
  </CardWithContent>

  <Footer price={currentPrice} />
</div>
