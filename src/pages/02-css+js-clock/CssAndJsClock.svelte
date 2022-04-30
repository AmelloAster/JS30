<script type="ts">
    import { onMount } from 'svelte';
    const handClass = 'h-[6px] absolute top-0 bottom-0 left-0 m-auto w-1/2 origin-[100%] rotate-90';

    onMount(() => {
        const secondHand = document.querySelector('#second-hand') as HTMLElement;
        const minuteHand = document.querySelector('#minute-hand') as HTMLElement;
        const hourHand = document.querySelector('#hour-hand') as HTMLElement;

        const handleSetDate = () => {
            const now = new Date();
            handleSetSeconds(now);
            handleSetMins(now);
            handleSetHours(now);
        };

        const handleSetSeconds = (now: Date) => {
            const seconds = now.getSeconds();
            const secondsDegrees = (seconds / 60) * 360 + 90;
            secondHand.style.transform = `rotate(${secondsDegrees}deg)`;
        };

        const handleSetMins = (now: Date) => {
            const mins = now.getMinutes();
            const minsDegrees = (mins / 60) * 360 + 90;
            minuteHand.style.transform = `rotate(${minsDegrees}deg)`;
        };

        const handleSetHours = (now: Date) => {
            const hours = now.getHours();
            const hoursDegrees = (hours / 12) * 360 + 90;
            hourHand.style.transform = `rotate(${hoursDegrees}deg)`;
        };

        setInterval(handleSetDate, 1000);
    });
</script>

<section
    class="bg-cover bg-center bg-[#018DED] bg-[url('https://unsplash.it/1500/1000?image=881&blur=5')] text-center text-sm w-full h-full"
>
    <div
        class="w-96 h-96 rounded-full relative top-[120px]  mx-auto border-[20px] border-teal-300 p-4"
    >
        <div class="relative w-full h-full translate-y-[-3px]">
            <div class={handClass + ' bg-rose-900'} id="hour-hand" />
            <div class={handClass + ' bg-rose-700'} id="minute-hand" />
            <div class={handClass + ' bg-rose-500'} id="second-hand" />
            <div class="absolute w-5 h-5 top-0 bottom-0 left-0 right-0 m-auto bg-black" />
        </div>
    </div>
</section>
