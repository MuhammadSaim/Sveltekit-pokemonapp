<script>

    import PokeCard from "../components/PokeCard.svelte";

    import { onMount } from "svelte";

    let pokemons = [];
    let isLoading = true;

    onMount(async () => {
        const pokemons_data = await fetch('https://pokeapi.co/api/v2/pokemon?limit=100');
        pokemons = await pokemons_data.json();
        pokemons = pokemons.results;
        isLoading = false;
    });
</script>


<div class="bg-white">
      <div class="mx-auto max-w-2xl px-4 py-16 sm:px-6 sm:py-24 lg:max-w-7xl lg:px-8">
        <h2 class="text-2xl font-bold tracking-tight text-gray-900 mb-4">Pokemons</h2>

        {#if isLoading}
            <div class="flex justify-center items-center">
                <div
            class="inline-block h-8 w-8 animate-spin rounded-full border-4 border-solid border-current border-r-transparent align-[-0.125em] text-primary motion-reduce:animate-[spin_1.5s_linear_infinite]"
            role="status">
            <span
                class="!absolute !-m-px !h-px !w-px !overflow-hidden !whitespace-nowrap !border-0 !p-0 ![clip:rect(0,0,0,0)]"
                >Loading...</span
            >
            </div>
            </div>
        {:else}
            <div class="grid grid-cols-1 gap-x-6 gap-y-10 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 xl:gap-x-8">
                {#each pokemons as pokemon, index}
                    <PokeCard pokemon={pokemon} index={index} />
                {/each}
            </div>
        {/if}
    </div>
</div>
