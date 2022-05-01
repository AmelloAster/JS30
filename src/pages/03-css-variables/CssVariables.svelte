<script type="ts">
    const handleUpdate = (e) => {
        const suffix = e.target.dataset.sizing || '';
        document.documentElement.style.setProperty(`--${e.target.name}`, e.target.value + suffix);
    };
</script>

<section class="w-full h-full pt-20 bg-[#193549] text-center' text-white text-3xl">
    <h2 class="text-center text-6xl mb-6">
        Update CSS Variables with <span class="hl">JS</span>
    </h2>
    <div class="controls flex justify-center items-center gap-6 mb-12">
        <div>
            <label for="spacing">Spacing: </label>
            <input
                on:change={handleUpdate}
                type="range"
                name="spacing"
                min="10"
                max="200"
                value="10"
                data-sizing="px"
            />
        </div>
        <div>
            <label for="blur">Blur: </label>
            <input
                on:change={handleUpdate}
                type="range"
                name="blur"
                min="0"
                max="25"
                value="10"
                data-sizing="px"
            />
        </div>
        <div>
            <label for="base">Base: </label>
            <input on:change={handleUpdate} type="color" name="base" value="#ffc600" />
        </div>
    </div>
    <div class="flex justify-center">
        <img src="https://source.unsplash.com/7bwQXzbF6KE/800x500" alt="target" />
    </div>
</section>

<style>
    :root {
        --base: #ffc600;
        --spacing: 10px;
        --blur: 10px;
    }
    .hl {
        color: var(--base);
    }
    img {
        padding: var(--spacing);
        background: var(--base);
        filter: blur(var(--blur));
    }
</style>
