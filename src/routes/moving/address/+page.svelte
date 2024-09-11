<script>
  import Header from "$lib/header.svelte";
  import Footer from "$lib/footer.svelte";
  import NavBtns from "$lib/navbtns.svelte";
  import HeadlineCard from "$lib/headlinecard.svelte";
  import { goto } from "$app/navigation";
  import Simplewrapper from "$lib/simplewrapper.svelte";

  let itemCount = 1; // Track the stepper count
  let totalPrice = 0; // Initialize total price
  $: totalPrice = itemCount === 0 ? 0 : 179 + (itemCount - 1) * 42;

  let multiselectedOptions = [];
  let currentPrice = "Total £99";

  function goToNextPage() {
    goto("/moving/contacts");
  }
  function goToPreviousPage() {
    goto("/moving/calendar");
  }
</script>

<!-- Main layout -->
<div class="flex flex-col gap-8">
  <Header price={currentPrice} />

  <HeadlineCard
    headline="Address"
    subheadline="Add where you'll be moving your items to and from"
    image="/img/assembly.svg"
    altText="Packing service"
  />

  <div class="flex flex-col gap-4">
    <Simplewrapper title="Collection postcode in the UK">
      <div class="mt-4 flex flex-col gap-2">
        <input
          type="text"
          placeholder="Collection postcode"
          class="w-full px-3 py-3 text-base rounded-lg border border-slate-300"
        />
        <input
          type="text"
          placeholder="Floor"
          class="w-fit px-3 py-3 text-base rounded-lg border border-slate-300"
        />
        <div>
          <label for="parking" class="flex items-center gap-2">
            <input name="parking" type="checkbox" />
            The apartment has a parking space close by that movers can use
          </label>
          <label for="parking" class="flex items-center gap-2">
            <input name="parking" type="checkbox" />
            Apartments with lift
          </label>
          <label for="parking" class="flex items-center gap-2">
            <input name="parking" type="checkbox" />
            Items need to be collected from an additional address
          </label>
        </div>
      </div>
    </Simplewrapper>

    <Simplewrapper title="Collection postcode in the UK">
      <div class="mt-4 flex flex-col gap-2">
        <input
          type="text"
          placeholder="Collection postcode"
          class="w-full px-3 py-3 text-base rounded-lg border border-slate-300"
        />
        <input
          type="text"
          placeholder="Floor"
          class="w-fit px-3 py-3 text-base rounded-lg border border-slate-300"
        />
        <div>
          <label for="parking" class="flex items-center gap-2">
            <input name="parking" type="checkbox" />
            The apartment has a parking space close by that movers can use
          </label>
          <label for="parking" class="flex items-center gap-2">
            <input name="parking" type="checkbox" />
            Apartments with lift
          </label>
          <label for="parking" class="flex items-center gap-2">
            <input name="parking" type="checkbox" />
            Items need to be collected from an additional address
          </label>
        </div>
      </div>
    </Simplewrapper>
    <div>
      <NavBtns nextAction={goToNextPage} prevAction={goToPreviousPage} />
    </div>
  </div>

  <Footer />
</div>
