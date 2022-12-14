<script>
  // import Github from "./Github.svelte";
  import GithubAwait from "./GithubAwait.svelte";
  import { setContext, onMount, afterUpdate } from "svelte";
  // components
  import Navbar from "./Navbar.svelte";
  import ExpensesList from "./ExpensesList.svelte";
  import Totals from "./Totals.svelte";
  import ExpenseForm from "./ExpenseForm.svelte";
  import Model from "./Model.svelte";
  // data
  // import expensesData from "./expenses";
  // variable
  let expenses = [];
  // set editing variables
  let setName = "";
  let setAmount = null;
  let setId = null;
  // toggle form variable
  let isFormOpen = false;
  // reactive
  $: isEditing = setId ? true : false;
  $: total = expenses.reduce((accumulator, current) => {
    return (accumulator += Number(current.amount));
  }, 0);
  // function
  let showForm = () => {
    isFormOpen = true;
  };

  let hideForm = () => {
    isFormOpen = false;
    setName = "";
    setAmount = null;
    setId = null;
  };

  // set local storage
  function setLocalStorege() {
    localStorage.setItem('expenses', JSON.stringify(expenses));
  };

  let removeExpense = id => {
    expenses = expenses.filter(item => item.id !== id);
  };

  let clearExpenses = () => {
    expenses = [];
  };

  function addExpense({ name, amount }) {
    let expense= { id: Math.random() * Date.now(), name, amount };
    console.log(typeof(expense.amount))
    expenses = [...expenses, expense];
  };

  let setModifiedExpense = id => {
    let expense = expenses.find(item => item.id === id);
    setId = expense.id;
    setName = expense.name;
    setAmount = expense.amount;
    showForm();
  };

  let editExpense = ({name, amount}) => {
    expenses = expenses.map(item => {
      return item.id === setId? { ...item, name, amount }:{ ...item };
    });
    setId = null;
    setName = "";
    setAmount = null;
    
  };

  // context
  /* const state = {
    name: "sample name",
    remove: removeExpense
  };
  setContext("state", state);  or */
  setContext("remove", removeExpense);
  setContext("modify", setModifiedExpense);

  onMount(() => {
    expenses = localStorage.getItem("expenses")
    ? JSON.parse(localStorage.getItem("expenses"))
    : [];
  });

  afterUpdate(() => {
    console.log("after update")
    setLocalStorege();
  })
</script>

<Navbar {showForm} />
<!-- <Github /> -->
<GithubAwait />

<!-- <main class="content">
  {#if isFormOpen}
    <Model>
      <ExpenseForm 
      {addExpense} 
      name={setName} 
      amount={setAmount} 
      {isEditing} 
      {editExpense} 
      {hideForm} />
    </Model>
  {/if}
  <Totals title="total expenses" {total}/>
  <ExpensesList {expenses} {removeExpense} />
  <button type="button" class="btn btn-primary btn-block" on:click={clearExpenses}>
    clear expenses
  </button>
</main> -->
<!-- <Model>
  <h1 slot="header"> hello</h1>
  <p slot="footer">Hoe are uou</p>
</Model> -->