<template>
  <div>
    <h3 class="mb-5">Alternativas:</h3>
    <v-expansion-panels>
      <v-expansion-panel v-for="(tienda, i) in tiendas" :key="i">
        <v-expansion-panel-header> {{tienda.nombre}} </v-expansion-panel-header>
        <v-expansion-panel-content>
          <v-list>
            <v-list-item-group color="primary">
              <v-list-item v-if="!tienda.datos">
                <v-list-item-content>
                  <v-list-item-title> No hay datos, prueba cambiando los términos de búsqueda </v-list-item-title>
                </v-list-item-content>
              </v-list-item>
              <v-list-item v-for="(item, j) in tienda.datos" :key="j">
                <v-list-item-avatar>
                  <v-img :src="item.Image"></v-img>
                </v-list-item-avatar>
                <v-list-item-content>
                  <v-list-item-title v-text="`${item.Nombre} / $${item.Precio}`"></v-list-item-title>
                </v-list-item-content>

                <v-list-item-icon>
                  <a
                    class="text-decoration-none"
                    :href="item.Url"
                    target="_blank"
                  >
                    <v-icon>mdi-launch</v-icon>
                  </a>
                </v-list-item-icon>
              </v-list-item>
            </v-list-item-group>
          </v-list>
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
  </div>
</template>

<script>
export default {
  props: ["alternativas", "cambia"],
  watch: {
    cambia() {
      console.log("cambio alternativas");
      this.tiendas[0].datos = this.alternativas["ml"];
      this.tiendas[1].datos = this.alternativas["ebay"];
      this.tiendas[2].datos = this.alternativas["olx"];
    },
  },
  data() {
    return {
      tiendas: [{ nombre:"Mercado Libre",datos:null},
                { nombre:"Ebay",datos:null},
                { nombre:"Olx",datos:null},],

    };
  },
};
</script>