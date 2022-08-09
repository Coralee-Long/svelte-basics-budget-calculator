<script>
  import { getContext } from "svelte";
  import Title from "./SectionTitle.svelte";
  export let name = ""; // empty string: falsey
  export let amount = null; // null: falsey
  export let isEditing;

  const { addExpense, editExpense, hideForm } = getContext("handlerFunctions");

  $: isEmpty = !name || !amount;
  $: buttonText = isEditing ? "Edit Expense" : "Add Expense";

  const formHandler = () => {
    if (isEditing) {
      editExpense({ name, amount });
    } else {
      addExpense({ name, amount });
    }
    name = "";
    amount = null;
  };
</script>

<section class="form">
  <Title title="Add Expense" />
  <form action="" class="expense-form" on:submit|preventDefault={formHandler}>
    <div class="form-control">
      <label for="name">Name</label>
      <input type="text" id="name" bind:value={name} />
    </div>
    <div class="form-control">
      <label for="amount">Amount</label>
      <input type="number" id="amount" bind:value={amount} />
    </div>
    {#if isEmpty}
      <p class="form-empty">Please fill out all fields</p>
    {/if}

    <button type="submit" class="btn btn-block" class:disabled={isEmpty}
      >{buttonText}
    </button>
    <button type="button" class="close-btn" on:click={hideForm}
      ><i class="fas fa-times" />Close</button
    >
  </form>
</section>
