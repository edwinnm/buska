<template>
  <div>
    <h3 class="mb-5">Comentarios:</h3>
 
          <v-list>
            <v-list-item-group color="primary">
              <v-list-item v-if="!comentarios">
                <v-list-item-content>
                  <v-list-item-title>No hemos podido encontrar comentarios </v-list-item-title>
                </v-list-item-content>
              </v-list-item>
              <v-list-item v-for="(item, j) in comentarios" :key="j">
                <v-list-item-content>
                  <v-list-item-title v-text="item"></v-list-item-title>
                </v-list-item-content>
              </v-list-item>
            </v-list-item-group>
          </v-list>
          <p class="red--text">
              {{parrafo}}
          </p>

  </div>
</template>

<script>
export default {
  props: ["comentarios","coincidencias"],
  computed:{
      parrafo(){
          return `Se han encontrado ${this.coincidencias} mensajes relacionados con términos de fraude.`;
      }
  }
};
</script>