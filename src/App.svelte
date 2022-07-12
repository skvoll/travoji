<script>
    import JsCookie from 'js-cookie';

    import {flags} from './lib/flags.ts';
    import Header from './lib/components/Header.svelte';
    import Country from './lib/components/Country.svelte';
    import FAB from './lib/components/FAB.svelte';
    import ResultModal from './lib/components/ResultModal.svelte';

    const saved = JsCookie.get('travoji');

    $: checked = saved ? saved.split('-') : [];
    $: search = '';
    $: modalIsOpened = false;
    $: aboutIsOpened = false;

    function onCountryClick(country) {
        search = '';
        const index = checked.indexOf(country);
        if (index !== -1) {
            checked.splice(index, 1);

            checked = [...checked];
        } else {
            checked = [...checked, country];
        }

        JsCookie.set('travoji', checked.join('-'));
    }
</script>

<section>
    <Header bind:searchValue={search} />
    <div class="list">
        {#each Object.entries(flags) as [flag, country]}
            {#if country.toUpperCase().indexOf(search.toUpperCase()) !== -1}
                <Country
                        {flag}
                        name={country}
                        checked={!!checked.includes(flag)}
                        on:click={() => onCountryClick(flag)}
                />
            {/if}
        {/each}
    </div>
    {#if Object.entries(checked).length > 0}
        <FAB bind:counter={checked.length} on:click={() => {modalIsOpened = true}}>🌐</FAB>
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
        padding: 12px 0 84px 0;
    }
</style>
