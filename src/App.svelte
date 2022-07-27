<script>
  // Imports
  import ExpenseForm from "./components/ExpenseForm.svelte";
  import { setContext } from "svelte";

  // Components
  import NavBar from "./components/NavBar.svelte";
  import ExpensesList from "./components/ExpensesList.svelte";
  import Totals from "./components/Totals.svelte";
  // Data
  import expensesData from "./data/expenses";
  import Expense from "./components/Expense.svelte";
  // Variables
  let expenses = [...expensesData];
  let totalExpenses;
  let name;
  let amount;
  let id;
  // Set Edit Variables
  let setName = "";
  let setAmount = null;
  let setId = null;
  // Reactive
  $: isEditing = setId ? true : false;
  $: totalExpenses = expenses.reduce((acc, curr) => {
    return (acc += curr.amount);
  }, 0);

  // Functions
  const removeExpense = (id) => {
    expenses = expenses.filter((item) => item.id !== id);
  };
  const clearExpenses = () => {
    expenses = [];
  };
  const addExpense = ({ name, amount }) => {
    let expense = { id: Math.random() * Date.now(), name, amount };
    expenses = [expense, ...expenses];
  };
  const setModifiedExpense = (id) => {
    let expense = expenses.find((item) => item.id === id);
    setName = expense.name;
    setAmount = expense.amount;
    setId = expense.id;
    isEditing = true; // Weird change I had to make since isEditing was false on first click of edit button
    console.log({ expense });
    console.log({ setName, setAmount, setId });
    console.log({ name, amount, id });
    console.log({ isEditing });
  };

  // Context set up so that all functions can be available in all components
  const handlerFunctions = {
    removeExpense: removeExpense,
    clearExpenses: clearExpenses, // (nameOfKey: functionName)
    addExpense: addExpense,
    setModifiedExpense: setModifiedExpense,
  };
  setContext("handlerFunctions", handlerFunctions);
</script>

<NavBar />
<main class="content">
  <ExpenseForm name={setName} amount={setAmount} />
  <Totals title="Total Expenses" {totalExpenses} />
  <ExpensesList {expenses} />
</main>
