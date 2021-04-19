<template>
  <v-card class="pa-3 ma-3">
    <h3>Información:</h3>
    <p class="font-weight-medium">
      <strong>{{ info.Ventas }}</strong><span> ventas concretadas</span>
    </p>
    <p class="font-weight-medium">
      <strong>{{ info.Recomendado }}</strong><span> de sus compradores lo recomienda.</span>
    </p>
    <p class="font-weight-medium">
      <strong>{{ info.Time }}</strong><span> {{ info.typeTime | tranformar }} vendiendo</span>
    </p>
  </v-card>
</template>

<script>
export default {
  props: ["info"],
  filters: {
    tranformar: function (value) {
      if (value === "anios") {
        return "años";
      } else if (value === "anio") {
        return "año";
      } else{
        return value;
      }

    },
  },
};
</script>
