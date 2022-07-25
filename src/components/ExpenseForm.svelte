<script>
  import Title from "./SectionTitle.svelte";
  let name = ""; // empty string: falsey
  let amount = null; // null: falsey

  $: isEmpty = !name || !amount;

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log("form submitted");
  };

  // If {name} is truthy, console log:
  // if (name) {
  //    console.log('name value is truthy');
  // };
</script>

<section class="form">
  <Title title="Add Expense" />
  <form action="" class="expense-form" on:submit={handleSubmit}>
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
