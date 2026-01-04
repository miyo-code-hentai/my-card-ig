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

				// show navbar + content + footer AFTER ripple done
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

	<!-- NAVBAR (SETELAH RIPPLE) -->
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

	<!-- FOOTER (SETELAH RIPPLE) -->
	{#if ready}
		<footer class="footer">
			<p>© 2026 Mi/Yo • and you gay</p>
		</footer>
	{/if}
</div>

<style>
	/* ===================== FOOTER BASE ===================== */
	.footer {
		position: fixed;
		bottom: 1rem;
		left: 50%;
		transform: translateX(-50%);

		color: rgba(255, 255, 255, 0.75);
		font-size: 0.8rem;
		letter-spacing: 0.02em;
		text-align: center;
		z-index: 5;

		opacity: 0;
		animation: footerIn 0.8s ease forwards;
		animation-delay: 0.2s;
	}

	@keyframes footerIn {
		to {
			opacity: 1;
		}
	}

	/* ===================== TABLET ===================== */
	@media (max-width: 900px) {
		.footer {
			font-size: 0.75rem;
			bottom: 0.8rem;
		}
	}

	/* ===================== MOBILE ===================== */
	@media (max-width: 640px) {
		.footer {
			font-size: 0.7rem;
			bottom: 4.5rem; /* aman dari bottom glass navbar */
			padding: 0 1rem;
			width: 100%;
		}
	}
</style>
