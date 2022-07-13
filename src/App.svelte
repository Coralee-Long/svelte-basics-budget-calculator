<script>
  import SectionTitle from "./components/SectionTitle.svelte";
  import NavBar from "./components/NavBar.svelte";
  import expensesData from "./data/expenses";
  import ExpensesList from "./components/ExpensesList.svelte";

  let expenses = [...expensesData];
  console.log(expenses);

  const removeExpense = (id) => {
    expenses = expenses.filter(item => item.id !== id);
  }
</script>


<NavBar />
<ExpensesList {expenses} {removeExpense}/>
