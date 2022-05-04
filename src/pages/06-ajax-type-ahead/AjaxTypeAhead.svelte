<script type="ts">
    interface CityItem {
        city: string;
        state: string;
        rank: number;
        population: number;
    }
    const endpoint =
        'https://gist.githubusercontent.com/Miserlou/c5cd8364bf9b2420bb29/raw/2bf258763cdddd704f8ffd3ea9a3e81d25e2c6f6/cities.json';
    let cities: CityItem[] = [];
    let filtersCities: CityItem[] = [];
    let searchInputValue = '';
    fetch(endpoint)
        .then((blob) => blob.json())
        .then((data) => cities.push(...data));
    const handleReset = () => {
        searchInputValue = '';
        filtersCities = [];
    };
    const numberWithCommas = (x: number) => {
        return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',');
    };

    const findMatches = (wordToMatch: string) => {
        return cities.filter((place) => {
            // here we need to figure out if the city or state matches what was searched
            const regex = new RegExp(wordToMatch, 'gi');
            return place.city.match(regex) || place.state.match(regex);
        });
    };

    const displayMatches = (target: CityItem) => {
        const regex = new RegExp(searchInputValue, 'gi');
        const cityName = target.city.replace(regex, `<span class="hl">${searchInputValue}</span>`);
        const stateName = target.state.replace(
            regex,
            `<span class="hl">${searchInputValue}</span>`,
        );
        return `<span class="name">${cityName}, ${stateName}</span>`;
    };

    const onChangeSearchInputValue = (e) => {
        searchInputValue = e.target.value;
        filtersCities = findMatches(searchInputValue);
    };
</script>

<section class="w-full h-full bg-yellow-400 pt-20">
    <button class="bg-white py-2 px-4 rounded mx-auto block mt-5" on:click={handleReset}
        >Reset</button
    >
    <form class="search-form">
        <input
            type="text"
            class="search"
            placeholder="Input City or State, and Click"
            value={searchInputValue}
            on:change={onChangeSearchInputValue}
        />
        <ul class="suggestions max-h-[40rem] overflow-hidden overflow-y-auto">
            {#if filtersCities.length === 0}
                <li>Filter for a city</li>
                <li>or a state</li>
            {/if}
            {#if filtersCities.length > 0}
                {#each filtersCities as item}
                    <li>
                        <span class="name">
                            {@html displayMatches(item)}
                        </span>
                        <span class="population">{numberWithCommas(item.population)}</span>
                    </li>
                {/each}
            {/if}
        </ul>
    </form>
</section>

<style global>
    .search-form input {
        width: 100%;
        padding: 20px;
    }

    .search-form input::placeholder {
        font-size: 24px;
    }

    .search-form {
        max-width: 400px;
        margin: auto;
    }

    .search-form input.search {
        margin: 0;
        text-align: center;
        outline: 0;
        border: 10px solid #f7f7f7;
        width: 120%;
        left: -10%;
        position: relative;
        top: 10px;
        z-index: 2;
        border-radius: 5px;
        font-size: 40px;
        box-shadow: 0 0 5px rgba(0, 0, 0, 0.12), inset 0 0 2px rgba(0, 0, 0, 0.19);
    }

    .suggestions {
        margin: 0;
        padding: 0;
        position: relative;
        /*perspective: 20px;*/
    }

    .suggestions li {
        background: white;
        list-style: none;
        border-bottom: 1px solid #d8d8d8;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.14);
        margin: 0;
        padding: 20px;
        transition: background 0.2s;
        display: flex;
        justify-content: space-between;
        text-transform: capitalize;
    }

    .suggestions li:nth-child(even) {
        transform: perspective(100px) rotateX(3deg) translateY(2px) scale(1.001);
        background: linear-gradient(to bottom, #ffffff 0%, #efefef 100%);
    }

    .suggestions li:nth-child(odd) {
        transform: perspective(100px) rotateX(-3deg) translateY(3px);
        background: linear-gradient(to top, #ffffff 0%, #efefef 100%);
    }

    .search-form span.population {
        font-size: 15px;
    }

    .search-form .hl {
        background: #ffc600;
    }
</style>
