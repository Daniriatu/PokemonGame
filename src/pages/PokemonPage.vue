<script src="./PokemonPage.ts" />

<template>
  <h1 v-if="!pokemon">Espere por favor ...</h1>
  <div v-else>
    <h1>¿Quién es este Pokemón?</h1>
    <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon" />
    <PokemonOptions :pokemons="pokemonArr" @selectionPokemon="checkAnswer" />
    <div v-if="showAnswer">
      <h2 class="fade-in">{{ message }}</h2>
      <button @click="newGame">Nuevo juego</button>
    </div>
  </div>
</template>

<style scoped></style>
