<script>
  import Header from "$lib/header.svelte";
  import Footer from "$lib/footer.svelte";
  import NavBtns from "$lib/NavBtns.svelte";

  import HeadlineCard from "$lib/HeadlineCard.svelte";
  import { goto } from "$app/navigation";
  import CalendarWithTimeIntervals from "$lib/CalendarWithTimeIntervals.svelte";
  import Calendar from "$lib/Calendar.svelte";
  import Timepill from "$lib/TimePill.svelte";
  import SimpleWrapper from "$lib/SimpleWrapper.svelte";

  let itemCount = 1; // Track the stepper count
  let totalPrice = 0; // Initialize total price
  $: totalPrice = itemCount === 0 ? 0 : 179 + (itemCount - 1) * 42;

  let currentPrice = "Total £99";

  function goToNextPage() {
    goto("/moving/address");
  }
  function goToPreviousPage() {
    goto("/moving/storagecollection");
  }

  let slotPosition = 1;
</script>

<!-- Main layout -->
<div class="flex flex-col gap-8">
  <Header price={currentPrice} />

  <HeadlineCard
    headline="Moving & cleaning date"
    subheadline="Please select the date is best for you"
    image="/img/assembly.svg"
    altText="Packing service"
  />

  <div class="flex flex-col gap-4">
    <SimpleWrapper title="When you want to move?">
      <div class="max-w-sm mx-auto">
        <CalendarWithTimeIntervals />
      </div>
    </SimpleWrapper>

    <SimpleWrapper
      title="End-of-tentancy cleaning"
      subheadline="We could clean only empty rooms."
    >
      <div class="max-w-sm mx-auto">
        <Calendar />
        <Timepill withTabs={false} />
      </div>
    </SimpleWrapper>

    <div>
      <NavBtns nextAction={goToNextPage} prevAction={goToPreviousPage} />
    </div>
  </div>

  <Footer />
</div>
