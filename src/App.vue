<template>
  <v-app>
    <v-app-bar
      app
      color="red"
      dark
    >
      <div class="d-flex align-center">

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/98/International_Pok%C3%A9mon_logo.svg/2560px-International_Pok%C3%A9mon_logo.svg.png"
          width="100"
        />
      </div>


    </v-app-bar>

    <v-main>
      <PokemonList/>
    </v-main>
  </v-app>
</template>

<script>
import PokemonList from './components/PokemonList';

export default {
  name: 'App',

  components: {
    PokemonList,
  },

  data: () => ({
    //
  }),
};
</script>