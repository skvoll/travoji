<script>
	export let flag;
	export let name;
	export let checked = false;
</script>

<section class:checked on:click>
	<div class="flag">{flag}</div>
	<div class="name">{name}</div>
	<div class="flag">{flag}</div>
</section>

<style>
	section {
		display: flex;
		min-height: 48px;
	}

	section.checked {
		background: aqua;
	}

	.flag {
		height: 48px;
		width: 48px;
		display: flex;
		align-items: center;
		justify-content: center;
		visibility: hidden;
	}

	section.checked > .flag {
		visibility: visible;
	}

	.name {
		flex: 1;
		display: flex;
		align-items: center;
		justify-content: center;
	}
</style>
