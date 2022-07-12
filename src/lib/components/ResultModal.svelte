<script>
	import { fade } from 'svelte/transition';

	export let flags = [];
	export let isOpened = false;

	$: result = flags.join('');

	function copy() {
		navigator.clipboard.writeText(result).then(() => isOpened = false).catch(() => null);
	}
</script>

{#if isOpened}
	<modal transition:fade={{ duration: 100 }}>
		<header>
			<button class="close" on:click={() => isOpened = false}>❌</button>
		</header>
		<section>{result}</section>
		<button class="copy" on:click={() => copy()}>COPY</button>
	</modal>
{/if}

<style>
	modal {
		position: fixed;
		height: 100vh;
		width: 100vw;
		background: white;
		display: flex;
		flex-direction: column;
	}

	modal section {flex: 1;
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 24px;
        font-size: 2em;
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
	}
</style>
