<script>
  import { getContext } from "svelte";
  import Title from "./SectionTitle.svelte";
  export let name = ""; // empty string: falsey
  export let amount = null; // null: falsey
  let isEditing;

  const { addExpense } = getContext("handlerFunctions");

  $: isEmpty = !name || !amount;
  $: buttonText = isEditing ? "Edit Expense" : "Add Expense";

  const formHandler = () => {
    addExpense({ name, amount });
    name = "";
    amount = null;
    console.log({ name, amount });
  };
  console.log({ isEditing });
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
    <button
      disabled={isEmpty}
      type="submit"
      class="btn btn-block"
      class:disabled={isEmpty}
      >{buttonText}
    </button>
    <button type="button" class="close-btn"
      ><i class="fas fa-times" />Close</button
    >
  </form>
</section>
