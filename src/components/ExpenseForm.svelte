<script>
  import Title from "./SectionTitle.svelte";
  let name = ""; // empty string: falsey
  let amount = null; // null: falsey

  $: isEmpty = !name || !amount;

  // Vanilla JS way to prevent Default on form:

  //   const formHandler = (e) => {
  //     e.preventDefault();
  //   };

  const formHandler = () => {
    console.log("form submitted");
    console.log({ name, amount });
    name = "";
    amount = null;
    console.log({ name, amount });
  };
</script>

<section class="form">
  <Title title="Add Expense" />
  <!-- // Vanilla JS way to prevent Default on form: -->
  <!-- <form action="" class="expense-form" on:submit={formHandler}> -->

  <!-- // Svelte in-line modifier method: -->
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
      class:disabled={isEmpty}>Add Expense</button
    >
    <button type="button" class="close-btn"
      ><i class="fas fa-times" />Close</button
    >
  </form>
</section>
