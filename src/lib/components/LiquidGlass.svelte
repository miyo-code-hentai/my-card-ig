<script lang="ts">
    import { spring } from "svelte/motion";
    import { onMount } from "svelte";

    export let width = "420px";
    export let height = "200px";
    export let padding = "2rem";
    export let center = true;
    export let mobileFull = true; // NEW

    const scale = spring(0.98, {
        stiffness: 0.06,
        damping: 0.25,
    });

    const y = spring(12, {
        stiffness: 0.06,
        damping: 0.25,
    });

    onMount(() => {
        scale.set(1);
        y.set(0);
    });
</script>

<div
    class="glass {center ? 'center' : ''} {mobileFull ? 'mobile-full' : ''}"
    style="
        width:{width};
        height:{height};
        padding:{padding};
        transform: translateY({$y}px) scale({$scale});
    "
>
    <slot />
</div>

<style>
    .glass {
        background: rgba(255, 255, 255, 0.18);
        backdrop-filter: blur(18px);
        -webkit-backdrop-filter: blur(18px);

        border-radius: 20px;
        border: 1px solid rgba(255, 255, 255, 0.35);
        box-shadow: 0 20px 50px rgba(0, 0, 0, 0.35);
        color: black;

        overflow-y: auto;
        overflow-x: hidden;

        /* smoother mobile scroll */
        -webkit-overflow-scrolling: touch;

        opacity: 0;
        animation: fadeIn 0.8s ease forwards;
    }

    .center {
        text-align: center;
    }

    /* ===== MOBILE ===== */
    @media (max-width: 768px) {
        .glass {
            width: calc(100vw - 2rem) !important;
            max-width: 100%;
            height: auto !important;
            max-height: 70vh;

            padding: 1.25rem;
            border-radius: 16px;
        }

        .mobile-full {
            margin: 1rem auto;
        }
    }

    /* ===== SCROLLBAR ===== */
    .glass::-webkit-scrollbar {
        width: 6px;
    }

    .glass::-webkit-scrollbar-track {
        background: transparent;
    }

    .glass::-webkit-scrollbar-thumb {
        background: rgba(255, 255, 255, 0.45);
        border-radius: 999px;
    }

    .glass::-webkit-scrollbar-thumb:hover {
        background: rgba(255, 255, 255, 0.65);
    }

    /* Firefox */
    .glass {
        scrollbar-width: thin;
        scrollbar-color: rgba(255, 255, 255, 0.45) transparent;
    }

    @keyframes fadeIn {
        to {
            opacity: 1;
        }
    }
</style>
