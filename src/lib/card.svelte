<script>
  export let title = "";
  export let description = "";
  export let isSelected = false;

  function toggleSelect() {
    isSelected = !isSelected;
  }
</script>

<div
  class="p-4 border rounded-lg cursor-pointer"
  on:click={toggleSelect}
  class:shadow={isSelected}
>
  <h3 class="font-bold">{title}</h3>
  <p>{description}</p>
</div>
