<script>
  import {getContext} from 'svelte';

  import {createEventDispatcher} from 'svelte';

  export let id;
  export let name = '';
  export let amount = 0;
  let displayAmount = false;

  const toggleCarat = () => {
    displayAmount = !displayAmount;
  }

  // const state = getContext('state');

  // const { anotherName, remove } = getContext()

    // create event dispatcher
    const dispatch = createEventDispatcher();

</script>

<article class="single-expense">
  <div class="expense-info">
    <h2>{name} 
      <button class="amount-btn" on:click|once={toggleCarat}>
      <i class='fas fa-caret-down'/>
    </button>
  </h2>
  {#if displayAmount}
  <h4>amount: ${amount}</h4>
  {/if}

  </div>
  <div class="expense-buttons">
    <button class="expense-btn edit-btn"><i class="fas fa-pen"></i></button>

    <!-- <button class="expense-btn delete-btn" on:click={() => remove(id)}><i class="fas fa-trash"></i></button> -->

    <!-- <button class="expense-btn delete-btn" on:click={() => dispatch('delete', id)}><i class="fas fa-trash"></i></button> -->

    <button class="expense-btn delete-btn" on:click={() => dispatch('delete', {id, name: 'hello from expense component'})}><i class="fas fa-trash"></i></button>
  </div>
</article>

