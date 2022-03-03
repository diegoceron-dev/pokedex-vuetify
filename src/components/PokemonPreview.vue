<template>
  <v-img 
    v-bind:src=image
    alt="no disponible"
    width="64px"> 
  </v-img>
</template>

<script lang="ts">
export default {
    name: "PokemonPreview",
    props: ['url'],
    mounted() {
      console.log(this.url)
      this.axios
      .get(this.url)
      .then((response) => {
          console.log(response);
          this.currentPokemon = response.data
          this.image = this.currentPokemon.sprites.front_default != null ? this.currentPokemon.sprites?.front_default: ""
      })
      .catch((error) => {
          console.log(error);
          this.errored = true;
      })
      .finally(() => (this.loading = false));
    },
    data:  () => ({
      currentPokemon: "",
      image: "", 
      errored: false
    })
}
</script>

<style>

</style>