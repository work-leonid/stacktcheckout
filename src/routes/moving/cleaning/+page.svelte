<script>
  import Header from "$lib/header.svelte";
  import Footer from "$lib/footer.svelte";

  import HeadlineCard from "$lib/HeadlineCard.svelte";
  import CardWithContent from "$lib/singleselectcardwithslot.svelte";

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
      title: "Cleaning for 2 bedrooms",
      description: "2 cleaners • 72h guarantee",
      price: "£229",
    },
  ];
  let cleaningSelectedOption = "Cleaning for 2 bedrooms";
  let slotPosition = 1;

  let allCleaningOptions = ["Kitchen", "Bathrooms", "Bedrooms", "Common areas"];
  const cleaningVariants = [
    {
      title: "Kitchen",
      image:
        "https://images.unsplash.com/photo-1507089947368-19c1da9775ae?q=80&w=3552&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
    },
    {
      title: "Bathrooms",
      image:
        "https://images.unsplash.com/photo-1620626011761-996317b8d101?q=80&w=3538&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
    },
    {
      title: "Bedrooms",
      image:
        "https://images.unsplash.com/photo-1522771739844-6a9f6d5f14af?q=80&w=3542&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
    },
    {
      title: "Common areas",
      image:
        "https://images.unsplash.com/photo-1502672260266-1c1ef2d93688?q=80&w=3000&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
    },
  ];
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
    {#if cleaningSelectedOption === "No, thank you"}{/if}

    {#if cleaningSelectedOption === "Cleaning for 2 bedrooms"}
      <div class="flex flex-col gap-4">
        <p class="">
          All our standard cleanings include dusting and washing of all
          reachable surfaces, wiping the outside of kitchen appliances &
          cabinets, basic cleaning of the bathrooms, and vacuuming & mopping of
          all floors
        </p>
        <div class="flex gap-2 *:shrink-0 overflow-x-scroll disable-scrollbars">
          {#each cleaningVariants as option}
            <div class="relative">
              <span
                class="bg-slate-900/90 px-3 py-1 rounded-full text-sm text-white absolute top-2 flex items-center gap-1 pl-2 left-2"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  viewBox="0 0 20 20"
                  fill="currentColor"
                  class="size-5"
                >
                  <path
                    fill-rule="evenodd"
                    d="M10 18a8 8 0 1 0 0-16 8 8 0 0 0 0 16Zm3.857-9.809a.75.75 0 0 0-1.214-.882l-3.483 4.79-1.88-1.88a.75.75 0 1 0-1.06 1.061l2.5 2.5a.75.75 0 0 0 1.137-.089l4-5.5Z"
                    clip-rule="evenodd"
                  />
                </svg>

                {option.title}</span
              >
              <img
                src={option.image}
                alt="Packing service"
                class="h-40 object-cover rounded-lg"
              />
            </div>
          {/each}
        </div>
      </div>
    {/if}
  </CardWithContent>

  <Footer />
</div>

<style>
  .disable-scrollbars::-webkit-scrollbar {
    background: transparent; /* Chrome/Safari/Webkit */
    width: 0px;
  }

  .disable-scrollbars {
    scrollbar-width: none; /* Firefox */
    -ms-overflow-style: none; /* IE 10+ */
  }
</style>
