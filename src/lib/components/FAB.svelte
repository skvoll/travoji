<script>
    import { fly } from 'svelte/transition';
</script>

<button transition:fly="{{ y: 100, duration: 400 }}" on:click><slot /></button>

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
</style>
