<script lang="ts">
	import { onMount } from "svelte";
	import { page } from "$app/state";
	import favicon from "$lib/assets/favicon.svg";
	import "../app.css";

	import GlassNavbar from "$lib/components/GlassNavbar.svelte";

	let { children } = $props();

	let loading = $state(true);
	let progress = $state(0);
	let ripple = $state(false);
	let ready = $state(false);

	onMount(() => {
		const interval = setInterval(() => {
			progress += 4;
			if (progress >= 100) {
				clearInterval(interval);
				loading = false;

				// start ripple
				setTimeout(() => (ripple = true), 300);

				// show navbar + content AFTER ripple done
				setTimeout(() => (ready = true), 5300);
			}
		}, 40);

		return () => clearInterval(interval);
	});
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
	<title>Mi/Yo</title>
</svelte:head>

<div class="page">
	<!-- RIPPLE BACKGROUND -->
	<div class="ripple {ripple ? 'active' : ''}">
		{#if ready}
			<div class="fade-in">
				{@render children()}
			</div>
		{/if}
	</div>

	<!-- NAVBAR (RENDER SETELAH RIPPLE) -->
	{#if ready}
		<GlassNavbar path={page.url.pathname} />
	{/if}

	<!-- LOADER -->
	{#if loading}
		<div class="loader">
			<div class="bar">
				<div class="fill" style="width:{progress}%"></div>
			</div>
		</div>
	{/if}
</div>

<footer class="footer">
	<p>@ 2026 and this is footer • and you gay</p>
</footer>

<style>
	.footer {
		position: fixed;
		bottom: 1rem;
		left: 50%;
		transform: translateX(-50%);
		color: rgba(255, 255, 255, 0.75);
		font-size: 0.8rem;
	}
</style>
