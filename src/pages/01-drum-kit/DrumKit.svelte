<script type="ts">
    import type { DrumKit } from './DrumKit.type';
    import { onMount } from 'svelte';

    const buttonList: DrumKit.ButtonListItem[] = [
        {
            keyName: 'A',
            dataKey: 65,
            musicalInstrument: 'CLAP',
        },
        {
            keyName: 'S',
            dataKey: 83,
            musicalInstrument: 'HIHAT',
        },
        {
            keyName: 'D',
            dataKey: 68,
            musicalInstrument: 'KICK',
        },
        {
            keyName: 'F',
            dataKey: 70,
            musicalInstrument: 'OPENHAT',
        },
        {
            keyName: 'G',
            dataKey: 71,
            musicalInstrument: 'BOOM',
        },
        {
            keyName: 'H',
            dataKey: 72,
            musicalInstrument: 'RIDE',
        },
        {
            keyName: 'J',
            dataKey: 74,
            musicalInstrument: 'SNARE',
        },
        {
            keyName: 'K',
            dataKey: 75,
            musicalInstrument: 'TOM',
        },
        {
            keyName: 'L',
            dataKey: 76,
            musicalInstrument: 'TINK',
        },
    ];
    const audioList: DrumKit.AudioListItem[] = [
        {
            dataKey: 65,
            src: 'src/assets/01-jdk/sounds/clap.wav',
        },
        {
            dataKey: 83,
            src: 'src/assets/01-jdk/sounds/hihat.wav',
        },
        {
            dataKey: 68,
            src: 'src/assets/01-jdk/sounds/kick.wav',
        },
        {
            dataKey: 70,
            src: 'src/assets/01-jdk/sounds/openhat.wav',
        },
        {
            dataKey: 71,
            src: 'src/assets/01-jdk/sounds/boom.wav',
        },
        {
            dataKey: 72,
            src: 'src/assets/01-jdk/sounds/ride.wav',
        },
        {
            dataKey: 74,
            src: 'src/assets/01-jdk/sounds/snare.wav',
        },
        {
            dataKey: 75,
            src: 'src/assets/01-jdk/sounds/tom.wav',
        },
        {
            dataKey: 76,
            src: 'src/assets/01-jdk/sounds/tink.wav',
        },
    ];
    const animationClass =
        ' transition-all scale-125 shadow-2xl shadow-yellow-400 border-yellow-400';
    const buttonClass =
        'key flex flex-col justify-center items-center px-4 py-2 rounded-md border-2 border-black text-white bg-[rgba(0,0,0,0.5)]';

    const startBeat = (dataKey: number) => {
        const audio = document.querySelector(`audio[data-key="${dataKey}"]`) as HTMLAudioElement;
        const key = document.querySelector(`button[data-key="${dataKey}"]`);
        if (!audio) return;
        audio.currentTime = 0;
        audio.play();
        key.className = buttonClass + animationClass;
    };

    const removeTransition = (e: TransitionEvent) => {
        // console.log(e);
        if (e.propertyName !== 'transform') return;
        (e.target as HTMLElement).className = buttonClass;
    };

    onMount(() => {
        const keys = document.querySelectorAll('.key');
        keys.forEach((key) => key.addEventListener('transitionend', removeTransition));
        window.addEventListener('keydown', (e) => {
            if (buttonList.some((i) => i.dataKey === e.keyCode)) {
                startBeat(e.keyCode);
            }
        });
    });
</script>

<section
    class="h-full flex justify-center items-center bg-[url('src/assets/01-jdk/background.jpg')]"
>
    <section class="flex gap-4">
        {#each buttonList as item}
            <button
                on:click={(e) => startBeat(item.dataKey)}
                data-key={item.dataKey}
                class={buttonClass}
            >
                <span>{item.keyName}</span>
                <span class="text-xs text-yellow-400">{item.musicalInstrument}</span>
            </button>
        {/each}
    </section>
    {#each audioList as item}
        <audio data-key={item.dataKey} src={item.src} />
    {/each}
</section>
