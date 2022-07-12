<script>
    import {fade} from 'svelte/transition';

    export let flags = [];
    export let isOpened = false;
    export let isCopied = false;

    $: result = `${flags.sort().join('')} #travoji`;

    function copy() {
        navigator.clipboard.writeText(result).then(() => {
            isCopied = true;

            setTimeout(() => {
                isOpened = false;
                isCopied = false;
            }, 1000);
        }).catch(() => null);
    }
</script>

{#if isOpened}
    <modal transition:fade={{ duration: 100 }}>
            <header>
                <button class="close" on:click={() => isOpened = false}>❌</button>
            </header>
            <section>
                {#if isCopied}
                    <span>COPIED TO CLIPBOARD!</span>
                {:else}
                    {result}
                {/if}
            </section>
            <button class="copy" on:click={() => copy()}>COPY</button>
    </modal>
{/if}

<style>
    modal {
        position: fixed;
        height: 100%;
        width: 100%;
        background: white;
        display: flex;
        flex-direction: column;
    }

    modal section {
        flex: 1;
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 24px;
        font-size: 2em;
    }

    modal span {
        text-align: center;
    }

    modal button {
        border: none;
        background: none;
    }

    modal button.close {
        --size: 64px;
        height: var(--size);
        width: var(--size);
        font-size: 32px;
    }

    modal button.copy {
        height: 64px;
        background: aquamarine;
        font-size: 2em;
    }
</style>
