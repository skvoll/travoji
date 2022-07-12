<script>
    import {fly} from 'svelte/transition';

    export let counter;
</script>

<button transition:fly="{{ y: 100, duration: 400 }}" on:click>
    <slot/>
    {#if counter}
        <span>{counter}</span>
    {/if}
</button>

<style>
    button {
        --size: 64px;
        --padding: 24px;
        bottom: var(--padding);
        right: var(--padding);
        height: var(--size);
        width: var(--size);
        position: fixed;
        border: none;
        border-radius: 50%;
        box-shadow: 4px 4px 12px rgba(0, 0, 0, 0.5);
        font-size: 2em;
        background: aquamarine;
    }

    button:active {
        box-shadow: none;
    }

    button > span {
        position: absolute;
        top: 0;
        right: 0;
        height: 24px;
        width: 24px;
        font-size: .5em;
        display: flex;
        align-items: center;
        justify-content: center;
        background: aqua;
        border-radius: 50%;
    }
</style>
