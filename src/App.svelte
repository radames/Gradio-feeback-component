<script lang="ts">
  import { onMount } from "svelte";

  let ratingDummy: HTMLInputElement;

  const ratings = [
    {
      label: "A",
      value: 1,
    },
    {
      label: "A",
      value: 0.5,
    },
    {
      label: "A",
      value: 0.25,
    },
    {
      label: "A",
      value: 0,
    },
    {
      label: "B",
      value: 0,
    },
    {
      label: "B",
      value: 0.25,
    },
    {
      label: "B",
      value: 0.5,
    },
    {
      label: "B",
      value: 1,
    },
  ];

  onMount(() => {
    ratingDummy = document.querySelector(
      "#rating-dummy textarea"
    ) as HTMLInputElement;
  });
  function buttonClick(rating) {
    console.log(rating);
    if(!ratingDummy) return;
    ratingDummy.value = JSON.stringify(rating);
    const event = new CustomEvent("input");
    ratingDummy.dispatchEvent(event);
  }
</script>

<div class="relative containerbg-white">
  <div class="flex">
    {#each ratings as rating, index}
      <button
        on:click={() => {
          buttonClick(rating);
        }}
        class="hover:bg-slate-400 font-bold py-2 px-4 border border-gray-400
        {index === 0 ? 'rounded-l-lg' : ''} {index === ratings.length - 1
          ? 'rounded-r-lg'
          : ''}"
        style="font-size: {(1 + rating.value) / 2}rem;"
      >
        {rating.label}
      </button>
    {/each}
  </div>
</div>

<style lang="postcss" scoped>
  .container :global(*) {
    color: black !important;
  }
</style>
