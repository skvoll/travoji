<script>
    export let searchValue;
</script>

<section>
    <label for="search">🔍</label>
    <input type="search" name="search" id="search" bind:value={searchValue}>
<!--    <span>❓</span>-->
</section>

<style>

    section {
        --height: 48px;
        --font-size: 32px;
        min-height: var(--height);
        display: flex;
        padding: 0 8px 0 8px;
        border-radius: 0 0 24px 24px;
        font-size: var(--font-size);
        background: aqua;
    }

    input {
        width: calc(100% - (var(--height) + var(--height) + 8px + 8px));;
        border: none;
        outline: none;
        box-sizing:border-box;
        -moz-box-sizing:border-box;
        font-size: inherit;
        text-align: center;
        text-transform: uppercase;
        background: inherit;
    }
</style>
