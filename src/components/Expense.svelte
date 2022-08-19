<script>
  import { getContext } from "svelte";
  	import { blur, slide, fly, scale, fade } from 'svelte/transition';

  export let id;
  export let name = "";
  export let amount = 0;
  let displayAmount = false;

  const toggleCarat = () => {
    displayAmount = !displayAmount;
  };

  const { removeExpense, setModifiedExpense } = getContext("handlerFunctions");
</script>

<article class="single-expense">
  <div class="expense-info">
    <h2>
      {name}
      <button class="amount-btn" on:click={toggleCarat}>
        <i class={displayAmount? "fas fa-caret-up" : "fas fa-caret-down" } />
      </button>
    </h2>
    {#if displayAmount}
      <h4 transition:slide>amount: ${amount}</h4>
    {/if}
  </div>
  <div class="expense-buttons">
    <button class="expense-btn edit-btn" on:click={() => setModifiedExpense(id)}
      ><i class="fas fa-pen" /></button
    >
    <button class="expense-btn delete-btn" on:click={() => removeExpense(id)}
      ><i class="fas fa-trash" /></button
    >
  </div>
</article>
