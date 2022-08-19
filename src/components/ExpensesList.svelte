<script>
  import Expense from "./Expense.svelte";
  import SectionTitle from "./SectionTitle.svelte";
  import { getContext } from "svelte";
  import {fly} from 'svelte/transition';
   import {flip} from 'svelte/animate';

  export let expenses = [];

  const { clearExpenses } = getContext("handlerFunctions");
</script>

<section class="content">
  <SectionTitle title="Expense List" />

  <ul>
    {#each expenses as expense, index (expense.id)}
    <div in:fly={{x: 200, delay: (index + 1) * 500}} out:fly={{x: -200}} animate:flip> 
      <Expense {...expense} />
      </div>
    {:else}
      <h2>Currently you have no expenses</h2>
    {/each}
  </ul>
  <button
    type="onSubmit"
    on:click={clearExpenses}
    class="btn btn-primary btn-block"
  >
    Clear Expenses
  </button>
</section>
