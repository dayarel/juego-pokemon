<template>
  <h1 v-if="!pokemon">Espere por favor...</h1>
  <div v-else>
    <h1>¿Quién es éste Pokémon</h1>

    <!-- TODO Imagen -->
    <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon" />

    <!-- TODO Opciones -->
    <PokemonOptions :pokemons="pokemonArr" @selection="checkAnswer($event)" />

    <template v-if="showAnswer" class="fadeIn">
      <h2>{{ message }}</h2>
      <button @click="newGame">Nuevo Juego</button>
    </template>
  </div>
</template>

<script>
import PokemonOptions from "@/components/PokemonOptions";
import PokemonPicture from "@/components/PokemonPicture";

import getPokemonOptions from "@/helpers/getPokemonOptions";

export default {
  components: { PokemonOptions, PokemonPicture },
  data() {
    return {
      pokemonArr: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: "",
    };
  },
  methods: {
    async mixPokemonArray() {
      this.pokemonArr = await getPokemonOptions();

      const rndInt = Math.floor(Math.random() * 4);
      this.pokemon = this.pokemonArr[rndInt];
    },
    checkAnswer(pokemonId) {
      this.showPokemon = true;
      pokemonId === this.pokemon.id
        ? (this.message = `Correcto!. El pokemon era ${this.pokemon.name}`)
        : (this.message = `Ups!!. El pokemon era ${this.pokemon.name}`);

      this.showAnswer = true;
    },
    newGame() {
      this.showPokemon = false;
      this.showAnswer = false;
      this.pokemonArr = [];
      this.pokemon = null;
      this.mixPokemonArray();
    },
  },
  mounted() {
    this.mixPokemonArray();
  },
};
</script>
