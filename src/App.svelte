<script>
  // Imports
  import ExpenseForm from "./components/ExpenseForm.svelte";
  import Modal from "./components/Modal.svelte"
  import { setContext, onMount, afterUpdate } from "svelte";

  // Components
  import NavBar from "./components/NavBar.svelte";
  import ExpensesList from "./components/ExpensesList.svelte";
  import Totals from "./components/Totals.svelte";

  // Data
  // import expensesData from "./data/expenses";

  // Variables
  // let expenses = [...expensesData];
  let expenses = [];
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

  // Toggle Form Variables
  let isFormOpen = false;

  // Functions
  const showForm = () => {
    isFormOpen = true;
  };
  const hideForm = () => {
    isFormOpen = false;
    setId = null;
    setName = "";
    setAmount = null;
  };

  const removeExpense = (id) => {
    expenses = expenses.filter((item) => item.id !== id);
   // setLocalStorage();  // Used afterUpdate() instead
  };
  const clearExpenses = () => {
    expenses = [];
  // setLocalStorage();  // Used afterUpdate() instead
  };
  const addExpense = ({ name, amount }) => {
    let expense = { id: Math.random() * Date.now(), name, amount };
    expenses = [expense, ...expenses];
    hideForm();
// setLocalStorage();  // Used afterUpdate() instead
  };
  const setModifiedExpense = (id) => {
    let expense = expenses.find((item) => item.id === id);
    setId = expense.id;
    setName = expense.name;
    setAmount = expense.amount;
    showForm();
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
    hideForm();
    // setLocalStorage();  // Used afterUpdate() instead
  };

  // Context set up so that all functions can be available in all components
  const handlerFunctions = {
    showForm: showForm,
    hideForm: hideForm,
    removeExpense: removeExpense,
    clearExpenses: clearExpenses, // (nameOfKey: functionName)
    addExpense: addExpense,
    setModifiedExpense: setModifiedExpense,
    editExpense: editExpense,
  };
  setContext("handlerFunctions", handlerFunctions);

  // Local Storage
   const setLocalStorage = () => {
    localStorage.setItem('expenses', JSON.stringify(expenses))
   };

   onMount(() => {
    expenses = localStorage.getItem('expenses') ? 
    JSON.parse(localStorage.getItem('expenses'))
    : []
   });

   // Can use afterUpdate() instead of having to use setLocalStorage after every function that edits the Expenses array 
   afterUpdate(() => {
    setLocalStorage();
   });
</script>


<NavBar />
<main class="content">
  {#if isFormOpen}
  <Modal>
    <ExpenseForm name={setName} amount={setAmount} {isEditing} />
    </Modal>
  {/if}
  <Totals title="Total Expenses" {totalExpenses} />
  <ExpensesList {expenses} />
</main>

 