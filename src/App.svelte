<script>
  import SectionTitle from "./components/SectionTitle.svelte";
  import NavBar from "./components/NavBar.svelte";
  import expensesData from "./data/expenses";
  import ExpensesList from "./components/ExpensesList.svelte";

  import {setContext} from 'svelte';

  const myStateObject = {
    name: 'some kind of value here',
    anotherName: 'another value here',
    remove: 'removeExpense'
  }

  let expenses = [...expensesData];
  console.log(expenses);

  const removeExpense = (id) => {
    expenses = expenses.filter(item => item.id !== id);
  }

  // context
  setContext('state', myStateObject);
</script>


<NavBar />
<ExpensesList {expenses}/>
