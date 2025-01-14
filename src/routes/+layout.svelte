<script lang="ts">
	import { browser } from '$app/environment';
	import Matrix from '$lib/elements/Matrix.svelte';
	import '../app.css';
	import { ModeWatcher } from 'mode-watcher';
	let { children } = $props();
</script>

<ModeWatcher defaultMode={'dark'} />

<div class="fixed -z-10 flex h-screen w-screen bg-black">
	{#if browser}
		<Matrix></Matrix>
	{/if}
</div>
<div class="flex h-screen w-screen items-center justify-center">
	{@render children()}
</div>
