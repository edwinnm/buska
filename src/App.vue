<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
    <v-toolbar-title>Buska</v-toolbar-title>
    <v-spacer></v-spacer>
        <router-link to="/" class="text-decoration-none">
          <v-btn text class="white--text">
          Inicio
          </v-btn>
        </router-link>
        <router-link to="/about" class="text-decoration-none">
          <v-btn text class="white--text">
          Acerca
          </v-btn>
        </router-link>
     </v-app-bar>

    <v-main class="mt-5">
      <v-container>
        <router-view/>

      </v-container>
    </v-main>

        <v-footer padless>
      
        <v-col class="primary lighten-1 py-4 text-center white--text"
        cols="12">
          {{ new Date().getFullYear() }} — <strong>edwinnm - Mauri C</strong>
        </v-col>
      
    </v-footer>
  </v-app>
</template>

<script>


export default {
  name: 'App',

  components: {
    
  },

  data: () => ({
    //
  }),
};
</script>
