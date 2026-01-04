<script lang="ts">
    export let path = "/";
</script>

<nav class="glass">
    <a href="/" class:active={path === "/"}>Home</a>
    <a href="/about" class:active={path === "/about"}>About</a>
    <a href="/gallery" class:active={path === "/gallery"}>Gallery</a>
    <a href="/contact" class:active={path === "/contact"}>Contact</a>
</nav>

<style>
    /* ===================== BASE ===================== */
    .glass {
        position: fixed;
        top: 1.4rem;
        left: 50%;
        transform: translateX(-50%) translateY(-10px);

        display: flex;
        gap: 3rem;
        padding: 0.6rem 4rem;

        background: rgba(255, 255, 255, 0.18);
        backdrop-filter: blur(18px);
        -webkit-backdrop-filter: blur(18px);

        border-radius: 20px;
        border: 1px solid rgba(255, 255, 255, 0.35);
        box-shadow: 0 20px 50px rgba(0, 0, 0, 0.35);

        opacity: 0;
        animation: navIn 1.2s ease forwards;
        z-index: 20;
    }

    @keyframes navIn {
        to {
            opacity: 1;
            transform: translateX(-50%) translateY(0);
        }
    }

    a {
        color: black;
        text-decoration: none;
        font-weight: 500;
        opacity: 0.75;
        position: relative;
        font-size: 0.95rem;
    }

    a.active {
        opacity: 1;
    }

    a.active::after {
        content: "";
        display: block;
        margin: 4px auto 0;
        width: 6px;
        height: 6px;
        background: black;
        border-radius: 50%;
    }

    /* ===================== TABLET ===================== */
    @media (max-width: 900px) {
        .glass {
            gap: 2rem;
            padding: 0.5rem 2.5rem;
        }
    }

    /* ===================== MOBILE ===================== */
    @media (max-width: 640px) {
        .glass {
            top: auto;
            bottom: 1rem;

            padding: 0.6rem 1.4rem;
            gap: 1.4rem;

            border-radius: 999px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.35);
        }

        a {
            font-size: 0.85rem;
        }

        a.active::after {
            width: 5px;
            height: 5px;
            margin-top: 3px;
        }
    }
</style>
