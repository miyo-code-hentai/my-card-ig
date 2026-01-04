<script>
    import LiquidGlass from "$lib/components/LiquidGlass.svelte";
    import img1 from "$lib/assets/img1.jpg";
    import img2 from "$lib/assets/img2.jpg";
    import img3 from "$lib/assets/img3.jpg";
    import img4 from "$lib/assets/img4.jpg";
    import img5 from "$lib/assets/img5.jpg";
</script>

<div class="top-right">
    <LiquidGlass width="1000px" height="400px" padding="1rem" center={false}>
        <h1>My Gallery</h1>
        <p>
            Here are some of my gooning collection some are in bad quality don't
            ask me why fix it yourself
        </p>

        <div class="bento">
            <div class="item tall">
                <img src={img1} alt="Gallery item 1" />
            </div>

            <div class="item wide">
                <img src={img2} alt="Gallery item 2" />
            </div>

            <div class="item">
                <img src={img3} alt="Gallery item 3" />
            </div>

            <div class="item">
                <img src={img4} alt="Gallery item 4" />
            </div>

            <div class="item wide">
                <img src={img5} alt="Gallery item 5" />
            </div>
        </div>
    </LiquidGlass>
</div>

<style>
    /* ===================== BASE (DESKTOP) ===================== */
    .bento {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        grid-auto-rows: 180px;
        gap: 12px;

        max-width: 100%;
        margin-top: 1rem;
    }

    .item {
        position: relative;
        overflow: hidden;
        border-radius: 16px;
        cursor: pointer;
    }

    .item img {
        width: 100%;
        height: 100%;
        object-fit: cover;

        transition:
            transform 0.6s ease,
            filter 0.6s ease;
    }

    /* Sizes */
    .tall {
        grid-row: span 2;
    }

    .wide {
        grid-column: span 2;
    }

    /* Hover */
    .item:hover img {
        transform: scale(1.1);
        filter: brightness(1.1);
    }

    /* ===================== TABLET ===================== */
    @media (max-width: 900px) {
        .bento {
            grid-template-columns: repeat(2, 1fr);
            grid-auto-rows: 200px;
        }

        .wide {
            grid-column: span 2;
        }

        .tall {
            grid-row: span 1;
        }
    }

    /* ===================== MOBILE ===================== */
    @media (max-width: 600px) {
        .bento {
            display: grid;
            grid-template-columns: 1fr;
            gap: 12px;

            /* 🔥 KEY FIX */
            grid-auto-rows: auto;
        }

        .item {
            aspect-ratio: 3 / 4; /* 🔥 CONSISTENT CARD SHAPE */
            border-radius: 14px;
        }

        .item img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        /* Reset desktop spans */
        .wide,
        .tall {
            grid-column: span 1;
            grid-row: span 1;
        }
    }
</style>
