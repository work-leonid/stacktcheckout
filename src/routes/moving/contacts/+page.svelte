<script>
  import Header from "$lib/header.svelte";
  import Footer from "$lib/footer.svelte";
  import NavBtns from "$lib/NavBtns.svelte";

  import HeadlineCard from "$lib/HeadlineCard.svelte";
  import { goto } from "$app/navigation";
  import SimpleWrapper from "$lib/SimpleWrapper.svelte";

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
    headline="Your contacts"
    subheadline="Please ensure that you provide us with both a valid telephone number and email address, as we will use them to verify order details and contact you on the date of service. "
    image="/img/contact.svg"
    altText="Packing service"
  />

  <div class="flex flex-col gap-4">
    <SimpleWrapper
      title="Our customer service team will contact you to finalise the details of your order"
      subheadline="If we are unable to reach you, we might have to reschedule or, in some instances, cancel the service. We want to avoid any inconvenience or potential additional costs for you."
    >
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
            Sign me up for early promotions and Stackt news
          </label>
          <label for="parking" class="flex items-center gap-2">
            <input name="parking" type="checkbox" />
            I agree with the Terms & Conditions, Privacy Policy and Cookie Preferences
          </label>
        </div>
      </div>
    </SimpleWrapper>

    <Footer />
    <div>
      <NavBtns
        text="Submit"
        nextAction={goToNextPage}
        prevAction={goToPreviousPage}
      />
    </div>
  </div>
</div>
