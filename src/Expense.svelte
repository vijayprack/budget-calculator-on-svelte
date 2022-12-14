<script>
    import { blur, slide, scale, fade, fly } from "svelte/transition";
    import { quintOut } from "svelte/easing";
    import { getContext } from 'svelte';
    // export let expense;
    // let { name, amount, id } = expense;

    // or
    export let id;
    export let name = "";
    export let amount = 0;
    let displayAmount = false;
    let toggleAmount = () => {
        displayAmount = !displayAmount;
    };
    // const { remove } = getContext("state");   or
    const removeExpense = getContext("remove");
    const setModifiedExpense = getContext("modify");
</script>

<article class="single-expense">
    <div class="expense-info">
        <h2>
            {name}
            <!-- on:click="{() => console.log("You click me")}" for writing javascript -->
            <button class="amount-btn" on:click={toggleAmount}> <!-- or  on:click|once={toggleAmount}  for one time -->
                <i class="fas fa-caret-down" />
            </button>
        </h2>
        {#if displayAmount}
            <!-- <h4 transition:blur>amount : ${amount}</h4> -->
            <!-- <h4 transition:scale>amount : ${amount}</h4> -->
            <h4 transition:slide>amount : ${amount}</h4>
            <!-- <h4 transition:fade>amount : ${amount}</h4> -->
            <!-- <h4 transition:fly={{ x:0, y:100, duration:2000, delay:500, easing:quintOut }} out:slide> -->
            <!-- amount : ${amount}</h4> -->
        {/if}
    </div>
    <div class="expense-buttons">
        <button class="expense-btn edit-btn" on:click={() => setModifiedExpense(id)}>
            <i class="fas fa-pen" />
        </button>
        <!-- on:click={() => remove(id)}     or -->
        <button class="expense-btn delete-btn"  on:click={() => removeExpense(id)}>
            <i class="fas fa-trash" />
        </button>
    </div>
</article>