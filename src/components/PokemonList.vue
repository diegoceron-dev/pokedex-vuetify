<template>
  <v-container class="grey lighten-5">
    <v-row>
      <v-col>
        <div class="grey--text mb-2">
          <h1>Pokedex</h1>
        </div>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-text-field label="Search pokemon" v-model="name"></v-text-field>
      </v-col>
      <v-col>
        <v-btn class="mx-2" fab dark large color="orange" @click="findPokemon">
          <v-icon dark> mdi-database-search </v-icon>
        </v-btn>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-simple-table style="padding-top: 2rem">
          <template v-slot:default>
            <thead>
              <tr>
                <th class="text-left">Pokemon</th>
                <th class="text-left">Preview</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="item in pokemons" :key="item.name">
                <td style="text-transform: capitalize">{{ item.name }}</td>
                <td><PokemonPreview :url="item.url" /></td>
              </tr>
            </tbody>
          </template>
        </v-simple-table>
        <div class="text-center" style="padding-top: 2rem">
          <v-pagination
            v-model="page"
            v-bind:length="totalPages"
            :total-visible="10"
            class="my-4"
            @input="next"
          ></v-pagination>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import PokemonPreview from "./PokemonPreview.vue";
export default {
  // el: "PokemonList"
  name: "PokemonList",
  data: () => ({
    pokemons: [],
    totalPages: 0,
    page: 1,
    itemsPerPage: 20,
    name: "",
  }),
  methods: {
    next(page) {
      const nextItems = this.itemsPerPage * page;
      this.axios
        .get("https://pokeapi.co/api/v2/pokemon/?limit=20&offset=" + nextItems)
        .then((response) => {
          this.pokemons = response.data.results;
          this.countPokemon = response.data.count;
          console.log(this.pokemons);
        });
    },
    findPokemon() {
      if (this.name) {
        console.log(this.name.toLowerCase())
        this.axios
          .get("https://pokeapi.co/api/v2/pokemon/" + this.name.toLowerCase())
          .then((response) => {
            this.pokemons = [];
            this.pokemons.push(response)
            this.countPokemon = 1;
            this.totalPages = 1;
            console.log(this.pokemons);
          });
      }
    },
  },
  mounted() {
    this.axios
      .get("https://pokeapi.co/api/v2/pokemon")
      .then((response) => {
        this.pokemons = response.data.results;
        this.totalPages = Math.trunc(response.data.count / this.itemsPerPage);
        console.log(this.pokemons);
      })
      .catch((error) => {
        console.log(error);
        this.errored = true;
      })
      .finally(() => (this.loading = false));
  },
  components: {
    PokemonPreview,
  },
};
</script>

<style>
</style>