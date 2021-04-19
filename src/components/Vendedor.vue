<template>
  <v-card elevation="2">
    <v-card-title color="primary" >
      <h3>
        <strong>Vendedor:</strong> <span>{{ info.Vendedor }}</span>
      </h3>
    </v-card-title>
    <v-row>
      <v-col cols="12" lg="9">
        <h3 class="pl-5">Calificaciones:</h3>
        <pie-chart :valores="info.Puntos"></pie-chart>
      </v-col>
      <v-col cols="12" lg="3" class="align-self-center">
        <vendedor-info :info="info.Informacion"></vendedor-info>
      </v-col>
    </v-row>
  </v-card>
</template>

<script>
import PieChart from "@/components/PieChart";
import VendedorInfo from "@/components/VendedorInfo";
export default {
  components: {
    PieChart,
    VendedorInfo,
  },
  props: ["info"],
};
</script>