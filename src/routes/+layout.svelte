<script lang="ts">
	import '@fontsource-variable/inter';
	import '../app.css';
	import Header from '$lib/components/Header.svelte';
</script>

<div class="app">
	<Header />

	<main class="main">
		<slot />
	</main>
</div>

<style>
	.app {
		width: 100%;
		height: 100dvh;
		display: flex;
		flex-direction: column;
		overflow-y: auto;
	}

	.main {
		width: 100%;
		height: 100%;
		display: flex;
		justify-content: center;
		align-items: flex-start;
		padding-inline: 30px;
		padding-block: 90px;
	}
</style>
