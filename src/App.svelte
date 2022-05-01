<script lang="ts">
    import { Router, Route, Link } from 'svelte-navigator';
    import DrumKitFC from './pages/01-drum-kit/DrumKit.svelte';
    import CssAndJsClockFC from './pages/02-css+js-clock/CssAndJsClock.svelte';
    import CssVariablesFC from './pages/03-css-variables/CssVariables.svelte';

    const linkClass = 'hover:text-blue-500 hover:underline';
</script>

<Router>
    <Route path="/">
        <section
            class="w-full h-full flex justify-center items-center flex-col bg-[url('https://images.unsplash.com/photo-1650617711972-d2be5861407a?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=872&q=80')] bg-no-repeat bg-center bg-cover"
        >
            <h1 class="text-white text-4xl">Aster's Javascript 30</h1>
            <section class="text-white mt-4 text-xl">
                <nav class="flex gap-6">
                    <Link class={linkClass} to="/drum-kit">Drum Kit</Link>
                    <Link class={linkClass} to="/css-js-clock">Css + Js Clock</Link>
                    <Link class={linkClass} to="/css-variables">Css Variables</Link>
                </nav>
            </section>
        </section>
    </Route>
</Router>
<Router>
    <header class="fixed w-full bg-white p-4 opacity-80">
        <nav class="flex gap-6">
            <Link class={linkClass} to="/">Home</Link>
            <Link class={linkClass} to="/drum-kit">Drum Kit</Link>
            <Link class={linkClass} to="/css-js-clock">Css + Js Clock</Link>
            <Link class={linkClass} to="/css-variables">Css Variables</Link>
        </nav>
    </header>
    <Route path="/drum-kit">
        <DrumKitFC />
    </Route>
    <Route path="/css-js-clock">
        <CssAndJsClockFC />
    </Route>
    <Route path="/css-variables">
        <CssVariablesFC />
    </Route>
</Router>
