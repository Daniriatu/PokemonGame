<script setup lang="ts">
import PokemonPicture from '../components/PokemonPicture.vue';
import PokemonOptions from '../components/PokemonOptions.vue';
import getPokemonOptions from '@/helpers/getPokemonOptions';
import type { Pokemon } from '../interfaces/pokemon';
import { ref } from 'vue';

const pokemonArr = ref<Pokemon[]>([]);

const pokemon = ref<Pokemon>();

const showPokemon = ref(false);

const showAnswer = ref(false);

const message = ref("");

const mixPokemonArray = async () => {
    pokemonArr.value = await getPokemonOptions();
    const randomInt = Math.floor(Math.random() * 4);
    pokemon.value = pokemonArr.value[randomInt];
    // console.log(randomInt);
    // console.log(pokemonArr.value);
}

// getPokemonOptions();
mixPokemonArray();

const checkAnswer = (selectedId: number) => {
    if (!pokemon.value) return;

    showAnswer.value = true;

    showPokemon.value = true;

    if (selectedId === pokemon.value.id) {
        message.value = `Correcto ${pokemon.value.name}`
    } else {
        message.value = `Oops, era, ${pokemon.value.name}`
    }

}

const newGame = () => {
    // console.log("Iniciar");
    window.location.reload();
}

</script>
<template>
    <h1 v-if="!pokemon">Espere por favor ...</h1>
    <div v-else>
        <h1>¿Quién es este Pokemón?</h1>
        <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon" />
        <PokemonOptions :pokemons="pokemonArr" @selectionPokemon="checkAnswer" />
        <div v-if="showAnswer">
            <h2 class="fade-in">{{ message }}</h2>
            <button @click="newGame">
                Nuevo juego
            </button>
        </div>
    </div>
</template>

<style scoped></style>