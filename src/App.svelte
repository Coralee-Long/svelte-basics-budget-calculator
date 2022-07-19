<script>
  import ExpenseForm from "./components/ExpenseForm.svelte";
  import { setContext } from "svelte";
  // Components
  import NavBar from "./components/NavBar.svelte";
  import ExpensesList from "./components/ExpensesList.svelte";
  import Totals from "./components/Totals.svelte";
  // Data
  import expensesData from "./data/expenses";
  // Variables
  let expenses = [...expensesData];
  let totalExpenses;
  // Reactive
  $: totalExpenses = expenses.reduce((acc, curr) => {
    // acc = acculmalator (total amount), curr = current (current amount);
    // console.log(`The current ACCULMULTOR is: ${acc}`);
    // console.log(`The CURRENT AMOUNT is: ${curr.amount}`);
    return (acc += curr.amount);
  }, 0);
  // Functions
  const removeExpense = (id) => {
    expenses = expenses.filter((item) => item.id !== id);
  };
  const clearExpenses = () => {
    expenses = [];
  };
  // Context set up so that all functions can be available in all components
  const handlerFunctions = {
    removeExpense: removeExpense,
    clearExpenses: clearExpenses, // (nameOfKey: functionName)
  };
  setContext("handlerFunctions", handlerFunctions);
</script>

<NavBar />
<main class="content">
  <ExpenseForm />
  <Totals title="Total Expenses" {totalExpenses} />
  <ExpensesList {expenses} />
</main>
