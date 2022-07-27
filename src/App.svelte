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
  // Set Edit Variables
  let editName = "";
  let editAmount = null;
  let editId = null;
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
  const addExpense = ({ name, amount }) => {
    let expense = { id: Math.random() * Date.now(), name, amount };
    expenses = [expense, ...expenses];
  };
  const editExpense = (id) => {
    let expense = expenses.find((item) => item.id === id);
    // console.log(expense);
    let editName = expense.name;
    let editAmount = expense.amount;
    let editId = expense.id;
    // console.log(editName, editAmount, editId);
    // console.log({ editName, editAmount, editId });
  };

  // Context set up so that all functions can be available in all components
  const handlerFunctions = {
    removeExpense: removeExpense,
    clearExpenses: clearExpenses, // (nameOfKey: functionName)
    addExpense: addExpense,
    editExpense: editExpense,
  };
  setContext("handlerFunctions", handlerFunctions);
</script>

<NavBar />
<main class="content">
  <ExpenseForm />
  <Totals title="Total Expenses" {totalExpenses} />
  <ExpensesList {expenses} />
</main>
