<template>
    <v-card elevation="3" >
        <v-img
        contain
        :src="url"
        >
     </v-img>
       <v-card-title color="primary"
      dark>
            {{nombre}}
        </v-card-title>
    </v-card>
</template>
<script>


export default {
    props: ["url", "nombre"]
}
</script>


