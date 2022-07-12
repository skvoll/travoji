<script>
    import {flags} from './lib/flags.ts';
    import Country from './lib/components/Country.svelte';
    import FAB from './lib/components/FAB.svelte';
    import ResultModal from './lib/components/ResultModal.svelte';

    $: checked = [];
    $: modalIsOpened = false;

    function onCountryClick(country) {
        const index = checked.indexOf(country);
        if (index !== -1) {
            checked.splice(index, 1);

            checked = [...checked];

            return;
        }

        checked = [...checked, country];
    }
</script>

<section>
    <div class="list">
        {#each Object.entries(flags) as [flag, country]}
            <Country
                    {flag}
                    name={country}
                    checked={!!checked.includes(flag)}
                    on:click={() => onCountryClick(flag)}
            />
        {/each}
    </div>
    {#if Object.entries(checked).length > 0}
        <FAB on:click={() => {modalIsOpened = true}}>🌐</FAB>
    {/if}
    <ResultModal bind:isOpened={modalIsOpened} flags={checked}/>
</section>

<style>
    section {
        flex: 1;
        max-height: 100vh;
        display: flex;
        flex-direction: column;
    }

    section > div.list {
        flex: 1;
        display: flex;
        overflow-y: scroll;
        flex-direction: column;
    }
</style>
