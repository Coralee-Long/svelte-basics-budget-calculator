<script>
  import Expense from "./Expense.svelte";
  import SectionTitle from "./SectionTitle.svelte";
  import {getContext} from 'svelte';

  export let expenses = [];

  const  {clearExpenses} = getContext('handlerFunctions');

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
  <button type='onSubmit' on:click={clearExpenses} class='btn btn-primary btn-block'>
    Clear Expenses
  </button>
</section>
