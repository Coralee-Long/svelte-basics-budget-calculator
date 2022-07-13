<script>
  import Expense from "./Expense.svelte";
  import SectionTitle from "./SectionTitle.svelte";

  export let expenses = [];
</script>

<section class='content'>
  <SectionTitle title="Expense List" />

  <ul>
    {#each expenses as expense}
      <Expense {...expense} />
    {:else}
      <h2>Currently you have no expenses</h2>
    {/each}
  </ul>
</section>
