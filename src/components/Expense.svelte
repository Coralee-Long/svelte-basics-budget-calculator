<script>
  import { getContext } from "svelte";

  export let id;
  export let name = "";
  export let amount = 0;
  let displayAmount = false;

  const toggleCarat = () => {
    displayAmount = !displayAmount;
  };

  const { removeExpense, editExpense } = getContext("handlerFunctions");
</script>

<article class="single-expense">
  <div class="expense-info">
    <h2>
      {name}
      <!-- <button class="amount-btn" on:click|once={toggleCarat}>    Example of a modifier ( once | ) -->
      <button class="amount-btn" on:click|once={toggleCarat}>
        <i class="fas fa-caret-down" />
      </button>
    </h2>
    {#if displayAmount}
      <h4>amount: ${amount}</h4>
    {/if}
  </div>
  <div class="expense-buttons">
    <button class="expense-btn edit-btn" on:click={() => editExpense(id)}
      ><i class="fas fa-pen" /></button
    >
    <button class="expense-btn delete-btn" on:click={() => removeExpense(id)}
      ><i class="fas fa-trash" /></button
    >
  </div>
</article>
