<script>
    import SectionTitle from "./Title.svelte";
    import Expense from "./Expense.svelte";
    import { fly } from "svelte/transition";
    import { flip } from "svelte/animate";
    export let expenses = [];
    // export let removeExpense;
</script>

<style>
    h2 {
        text-transform: capitalize;
    }
</style>

<section>
    <SectionTitle title="expense list" />
    <ul>
        {#each expenses as expense, index(expense.id)}
            <!-- <Expense {expense}/> -->
            <div in:fly={{ x : 300, delay : (index + 1) * 700 }} 
            out:fly={{ x : -300 }} animate:flip >
                <Expense  {...expense} />  <!-- or add {removeExpence} -->
            </div> 
        {:else}
            <h2>currentely you have no expenses</h2>
        {/each}
    </ul>
</section>