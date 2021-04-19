<template>
  <div>
    <v-card class="mx-auto" max-width="400" tile>
      <v-card-title>
        <h1 class="my-4">Buska</h1>
      </v-card-title>
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title>Descripción</v-list-item-title>
          <div style="font-size: 0.875rem; color: rgba(0, 0, 0, 0.6)">
            Buska utiliza webScraping para obtener la información relevante de
            un vendedor de "Mercado libre", con el propósito de corroborar su
            integridad, posterior verifica el mismo producto en otras tiendas
            online para realizar una comparativa de precios.
          </div>
        </v-list-item-content>
      </v-list-item>
      <v-list-item two-line>
        <v-list-item-content>
          <v-list-item-title>Fuente de datos</v-list-item-title>
          <v-list-item-subtitle>Mercado Libre, Ebay, Olx</v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-list-item three-line>
        <v-list-item-content>
          <v-list-item-title>Tecnologías</v-list-item-title>
          <v-list-item-subtitle
            ><strong>Backend:</strong> Flask, Beautifulsoup -
            Heroku</v-list-item-subtitle
          >
          <v-list-item-subtitle
            ><strong>Frontend:</strong> VueJs, Vuetify, ChatJs -
            GithubPages</v-list-item-subtitle
          >
        </v-list-item-content>
      </v-list-item>
    </v-card>
  </div>
</template>
