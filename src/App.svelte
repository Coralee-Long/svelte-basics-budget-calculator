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
    setId = expense.id;
    setName = expense.name;
    setAmount = expense.amount;
  };
  const editExpense = ({ name, amount }) => {
    expenses = expenses.map((item) => {
      if (item.id === setId) {
        return { ...item, name, amount };
      } else {
        return item;
      }
    });
    setId = null;
    setName = "";
    setAmount = null;
  };

  // Context set up so that all functions can be available in all components
  const handlerFunctions = {
    removeExpense: removeExpense,
    clearExpenses: clearExpenses, // (nameOfKey: functionName)
    addExpense: addExpense,
    setModifiedExpense: setModifiedExpense,
    editExpense: editExpense,
  };
  setContext("handlerFunctions", handlerFunctions);
</script>

<NavBar />
<main class="content">
  <ExpenseForm name={setName} amount={setAmount} {isEditing} />
  <Totals title="Total Expenses" {totalExpenses} />
  <ExpensesList {expenses} />
</main>
