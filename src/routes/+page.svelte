<script>
    import LiquidGlass from "$lib/components/LiquidGlass.svelte";
</script>

<div class="top-right">
    <LiquidGlass width="1000px" height="400px" padding="2rem" center={false}>
        <div class="profile">
            <img src="gudako.jpg" class="avatar" alt="Gudako" />
            <div class="intro">
                <h1>Hi I'm <span class="highlight">Miyo</span></h1>
            </div>
        </div>
        <p>
            Hi. I make things move, break, and somehow function. I obsess over
            smooth transitions, fight invisible layout bugs, and spend hours
            fixing something no one will notice. This is not a portfolio — it’s
            a documented mental state.
        </p>
    </LiquidGlass>
</div>

<style>
    .highlight {
        color: aqua;
    }

    .avatar {
        width: 120px;
        height: 120px;
        border-radius: 50%;
        object-fit: cover; /* penting biar nggak gepeng */
    }

    .profile {
        display: flex;
        align-items: center;
        gap: 20px;
    }
</style>
