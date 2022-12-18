<script>
    import { blur, fade, fly } from "svelte/transition";
</script>

<div class="modal-container" in:blur out:fade>
    <div class="modal-content" transition:fly={{y:100}}>
        <slot></slot>
        <!-- <h3>hello from model</h3>
        <h2> bybye</h2>
        <slot name="header"></slot>
        <slot name="footer"></slot> -->
    </div>
</div>