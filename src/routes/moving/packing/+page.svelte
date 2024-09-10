<script>
  import Header from "$lib/Header.svelte";
  import Footer from "$lib/Footer.svelte";

  import HeadlineCard from "$lib/HeadlineCard.svelte";
  import CardWithStepper from "$lib/CardWithStepper.svelte";
  import CardWithContent from "$lib/SingleSelectCardWithSlot.svelte";
  import MultiSelectCard from "$lib/MultiSelectCard.svelte";
  import CustomCard from "$lib/CustomCard.svelte";
  import Stepper from "$lib/Stepper.svelte";
  import { goto } from "$app/navigation";

  let itemCount = 1; // Track the stepper count
  let totalPrice = 0; // Initialize total price
  $: totalPrice = itemCount === 0 ? 0 : 179 + (itemCount - 1) * 42;

  let multiselectedOptions = [];
  let currentPrice = "Total: one-time £99, per week £19.9";

  function goToNextPage() {
    goto("/moving/cleaning");
  }
  function goToPreviousPage() {
    goto("/moving/flat");
  }

  const benefits = [
    "Proffessional packing materials",
    "Safe and secure moving and storing",
    "Save your time and money",
  ];
  const additionalServices = [
    {
      title: "Unpacking for your items",
      description: "We will carefully unpack all your items after delivery.",
      price: "£169",
    },
  ];
  const packingMeterials = [
    {
      title: "Small boxes",
      description: "36cm x 36cm x36cm -14inch (up to 15kg)",
      price: "£2.72/box",
      image: "/packing/materials/smallbox.svg",
    },
    {
      title: "Large boxes",
      description: "46 × 46 × 46cm -18 inches (up to 20kg)",
      price: "£2.72/box",
      image: "/packing/materials/largebox.svg",
    },
    {
      title: "Wardrobe boxes",
      description: "holds 20-30 hangers",
      price: "£8.1/box",
      image: "/packing/materials/wardrobebox.svg",
    },
    {
      title: "Tape",
      description: "Brown PVC tape: 5cm x 6600cm",
      price: "£2.72/tape",
      image: "/packing/materials/tape.svg",
    },
    {
      title: "Bubble wrap(s)",
      description: "30cm x 50m roll",
      price: "£40/roll",
      image: "/packing/materials/bubblewrap.svg",
    },
    {
      title: "Paper pack",
      description: "White packing paper pack",
      price: "£11/box",
      image: "/packing/materials/paper.svg",
    },
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
      title: "Proffesional packing materials",
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
  let materialsOptions = [
    "30 small boxes",
    "15 large boxes",
    "10 wardrobe boxes",
    "2 bubble wraps",
    "17 tapes",
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
      <div class="flex flex-col gap-2">
        <h3 class="text-xl font-semibold">Additional services</h3>
        <MultiSelectCard
          options={additionalServices}
          bind:multiselectedOptions
        />
      </div>
    {/if}

    {#if packingSelectedOption === "All-inclusive packing"}
      <CustomCard
        headline="Professional packing with all-inclusive materials"
        subheadline="We will carefully pack all your items in one go in the safest way possible. You'll get unlimited packing materials included."
        image="/img/packing/bighouse.svg"
        altText="Packing service"
      >
        <div class="flex gap-1 flex-wrap">
          {#each allInclusiveOptions as option}
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
        <div class="flex flex-col gap-2">
          <h3 class="text-base sm:text-xl font-semibold">
            Additional services
          </h3>
          <MultiSelectCard
            options={additionalServices}
            bind:multiselectedOptions
          />
        </div>
      </CustomCard>
    {/if}

    {#if packingSelectedOption === "Professional packing service"}
      <div class="flex flex-col gap-2">
        <h3 class="text-xl font-semibold">Additional services</h3>
        <MultiSelectCard
          options={additionalServices}
          bind:multiselectedOptions
        />
      </div>
      <div class="flex flex-col gap-2 mt-4">
        <h3 class="text-xl font-semibold">Proffesional packing materials</h3>
        <p>For a 2 bedrooms apartment our clients normally need</p>
        <div class="flex gap-1 flex-wrap">
          {#each materialsOptions as option}
            <span
              class="flex bg-orange-100 ring-1 ring-orange-200 font-semibold w-fit pl-1 pr-2 py-0.5 rounded-full text-sm gap-0.5 text-orange-600 items-center"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 16 16"
                fill="currentColor"
                class="size-4 text-orange-600"
              >
                <path
                  fill-rule="evenodd"
                  d="M8 15A7 7 0 1 0 8 1a7 7 0 0 0 0 14Zm.75-10.25v2.5h2.5a.75.75 0 0 1 0 1.5h-2.5v2.5a.75.75 0 0 1-1.5 0v-2.5h-2.5a.75.75 0 0 1 0-1.5h2.5v-2.5a.75.75 0 0 1 1.5 0Z"
                  clip-rule="evenodd"
                />
              </svg>

              {option}</span
            >
          {/each}
        </div>

        <CardWithStepper options={packingMeterials} />
      </div>
    {/if}

    {#if packingSelectedOption === "Packing by furniture"}
      <CustomCard
        headline="How much furniture must be packed?"
        subheadline="We'll use professional packing materials to pack your furniture in the safest way possible."
        image="/img/packing/big.svg"
        altText="Packing service"
      >
        <Stepper bind:count={itemCount} min={1} />
        <div>
          <p class="text-xl font-semibold">
            Total: <span class="text-orange-600">£{totalPrice}</span>
          </p>
          <p class="text-sm">
            Includes high quality packing materials and proffesional packing
            service
          </p>
        </div>
        <div class="flex flex-col gap-2 mt-4">
          <h3 class="text-xl font-semibold">Additional services</h3>
          <MultiSelectCard
            options={additionalServices}
            bind:multiselectedOptions
          />
        </div>
        <div class="flex flex-col gap-2 mt-4">
          <h3 class="text-xl font-semibold">Proffesional packing materials</h3>
          <p>For a 2 bedrooms apartment our clients normally need</p>
          <div class="flex gap-1 flex-wrap">
            {#each materialsOptions as option}
              <span
                class="flex bg-orange-100 ring-1 ring-orange-200 font-semibold w-fit pl-1 pr-2 py-0.5 rounded-full text-sm gap-0.5 text-orange-600 items-center"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  viewBox="0 0 16 16"
                  fill="currentColor"
                  class="size-4 text-orange-600"
                >
                  <path
                    fill-rule="evenodd"
                    d="M8 15A7 7 0 1 0 8 1a7 7 0 0 0 0 14Zm.75-10.25v2.5h2.5a.75.75 0 0 1 0 1.5h-2.5v2.5a.75.75 0 0 1-1.5 0v-2.5h-2.5a.75.75 0 0 1 0-1.5h2.5v-2.5a.75.75 0 0 1 1.5 0Z"
                    clip-rule="evenodd"
                  />
                </svg>

                {option}</span
              >
            {/each}
          </div>

          <CardWithStepper options={packingMeterials} />
        </div>
      </CustomCard>
    {/if}
    {#if packingSelectedOption === "Proffesional packing materials"}
      <div class="flex flex-col gap-2 mt-4">
        <h3 class="text-xl font-semibold">Proffesional packing materials</h3>
        <p>For a 2 bedrooms apartment our clients normally need</p>
        <div class="flex gap-1 flex-wrap">
          {#each materialsOptions as option}
            <span
              class="flex bg-orange-100 ring-1 ring-orange-200 font-semibold w-fit pl-1 pr-2 py-0.5 rounded-full text-sm gap-0.5 text-orange-600 items-center"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 16 16"
                fill="currentColor"
                class="size-4 text-orange-600"
              >
                <path
                  fill-rule="evenodd"
                  d="M8 15A7 7 0 1 0 8 1a7 7 0 0 0 0 14Zm.75-10.25v2.5h2.5a.75.75 0 0 1 0 1.5h-2.5v2.5a.75.75 0 0 1-1.5 0v-2.5h-2.5a.75.75 0 0 1 0-1.5h2.5v-2.5a.75.75 0 0 1 1.5 0Z"
                  clip-rule="evenodd"
                />
              </svg>

              {option}</span
            >
          {/each}
        </div>
        <CardWithStepper options={packingMeterials} />
      </div>
    {/if}
  </CardWithContent>

  <Footer price={currentPrice} />
</div>
