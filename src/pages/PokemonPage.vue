<template>
  <h1>¿Quién es éste Pokémon</h1>

  <!-- TODO Imagen -->
  <PokemonPicture />

  <!-- TODO Opciones -->
  <PokemonOptions />
</template>

<script>
import PokemonOptions from "@/components/PokemonOptions";
import PokemonPicture from "@/components/PokemonPicture";
export default {
  components: { PokemonOptions, PokemonPicture },
};
</script>
