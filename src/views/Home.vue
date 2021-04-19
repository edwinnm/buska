<template>
  <div>
    <v-row class="px-5">
      <v-text-field
        label="Url del producto"
        placeholder="https://articulo.mercadolibre.com.ec/tuarticulo"
        v-model="url"
        v-on:keyup.13="cargarDatosIniciales"
      ></v-text-field>
    </v-row>
    <div v-if="fullData">
      <v-row>
        <v-col sm="5" class="align-self-center">
          <product :url="fullData.Image" :nombre="fullData.Nombre"></product>
        </v-col>
        <v-spacer></v-spacer>
        <v-col sm="7">
          <vendedor :info="info"> </vendedor>
        </v-col>
      </v-row>

      <v-card class="pa-5 my-10">
        <v-row>
          <v-col cols="12" md="8">
            <v-text-field
              label="Nombre del producto"
              v-model="nombreProducto"
              hint="Busca en otras tiendas como Ebay y Olx"
              persistent-hint
            ></v-text-field>
            <v-spacer></v-spacer>
          </v-col>
          <v-col col="6" md="2" class="align-self-center">
            <v-btn @click="cargarDatosBarra">Buscar</v-btn>
          </v-col>
          <v-col col="6" md="2" class="align-self-center">
            <ul class="miLista">
              <li>
                <v-img
                  src="@/assets/img/ml.png"
                  max-height="32"
                  max-width="32"
                  :class="claseMl"
                ></v-img>
              </li>
              <li>
                <v-img
                  src="@/assets/img/ebay.png"
                  max-height="32"
                  max-width="32"
                  :class="claseEbay"
                ></v-img>
              </li>
              <li>
                <v-img
                  src="@/assets/img/olx.png"
                  max-height="32"
                  max-width="32"
                  :class="claseOlx"
                ></v-img>
              </li>
            </ul>
          </v-col>
        </v-row>
        <v-row>
          <v-col class="small">
            <bar-chart
              class="small"
              :datos="datosBarras"
              :cambia="cambia"
            ></bar-chart>
          </v-col>
        </v-row>
      </v-card>

      <v-row>
        <v-col>
          <alternatives
            :alternativas="datosAlternativas"
            :cambia="cambia"
          ></alternatives>
        </v-col>
      </v-row>
    </div>
    <div v-if="cargandoDatosIniciales && !errorIniciales" class="contenedor">
      <v-progress-circular
        :size="150"
        color="primary"
        indeterminate
        class="centrado"
      ></v-progress-circular>
    </div>
    <div v-if="errorIniciales" class="contenedor">
      <v-row>
        <v-col class="align-self-center">
          <v-img src="@/assets/img/404.png"> </v-img>
        </v-col>
        <v-col class="align-self-center">
          <h2>Opss!! Ocurre más a menudo de lo que piensas.</h2>
          <h4>Por favor: revisa la url o llama al ingeniero más cercano.</h4>
          <small
            >Imagen tomada de:
            <a href="https://www.freepng.es/png-3lwyot/" target="_blank"
              >freepng</a
            >
          </small>
        </v-col>
      </v-row>
    </div>
  </div>
</template>

<style scoped>
.buscando {
  
  animation-name: parpadeo;
  animation-duration: 1s;
  animation-timing-function: linear;
  animation-iteration-count: infinite;

  -webkit-animation-name:parpadeo;
  -webkit-animation-duration: 1s;
  -webkit-animation-timing-function: linear;
  -webkit-animation-iteration-count: infinite;
}
.encontrado {
  filter: none;
}
.noEncontrado {
  filter: grayscale(1);
}

.miLista {
  list-style-type: none;
  margin: 0;
  padding: 0;
  display: flex;
}
.miLista li {
  padding: 7px;
}

.contenedor {
  height: 70vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.small {
  width: "100%";
  position: "relative";
  max-height: 400px;
}

/* Parpadeo */
@-moz-keyframes parpadeo{  
  0% { opacity: 1.0; }
  50% { opacity: 0.0; }
  100% { opacity: 1.0; }
}

@-webkit-keyframes parpadeo {  
  0% { opacity: 1.0; }
  50% { opacity: 0.0; }
   100% { opacity: 1.0; }
}

@keyframes parpadeo {  
  0% { opacity: 1.0; }
   50% { opacity: 0.0; }
  100% { opacity: 1.0; }
}
</style>


<script>
// // @ is an alias to /src

import Product from "@/components/Product";
import Vendedor from "@/components/Vendedor";
import BarChart from "@/components/BarChart";
import Alternatives from "@/components/Alternatives";

export default {
  name: "Home",
  components: {
    Vendedor,
    Product,
    BarChart,
    Alternatives,
  },
  data() {
    return {
      url: "",
      cambia: "",
      nombreProducto: "",
      fullData: null,
      datosBarras: null,
      cargandoDatosIniciales: false,
      errorIniciales: false,
      datosAlternativas: null,
      mlCargado: false,
      ebayCargado: false,
      olxCargado: false,
      errorEbay: false,
      errorOlx: false,
    };
  },
  computed: {
    info() {
      return {
        Vendedor: this.fullData.Vendedor,
        Puntos: this.fullData.Puntos,
        Informacion: {
          Ventas: this.fullData.Ventas,
          Recomendado: this.fullData.Recomendado,
          Time: this.fullData.Time,
          typeTime: this.fullData.typeTime,
        },
      };
    },
    claseMl() {
      if (this.mlCargado) {
        return "encontrado";
      } else if (this.errorIniciales) {
        return "noEncontrado";
      } else {
        return "buscando";
      }
    },
    claseEbay() {
      if (this.ebayCargado) {
        return "encontrado";
      } else if (this.errorEbay) {
        return "noEncontrado";
      } else {
        return "buscando";
      }
    },
    claseOlx() {
      if (this.olxCargado) {
        return "encontrado";
      } else if (this.errorOlx) {
        return "noEncontrado";
      } else {
        return "buscando";
      }
    },
  },
  methods: {
    cargarDatosIniciales() {
      this.fullData = null;
      this.datosBarras = null;
      this.cargandoDatosIniciales = true;
      this.errorIniciales = false;
      this.mlCargado = false;
      this.url = this.url.substring(0,this.url.indexOf("_JM")+3)
      fetch("https://serverweb2.herokuapp.com/search?url=" + this.url)
        .then((response) => response.json())
        .then((result) => {
          this.fullData = result;
          this.nombreProducto = this.fullData.Nombre;
          this.datosBarras = {
            ml: [
              this.fullData.Maximo,
              this.fullData.Promedio,
              this.fullData.Minimo,
            ],
          };
          this.datosAlternativas = { ml: this.fullData.otrosDatos };
          this.cargandoDatosIniciales = false;
          this.mlCargado = true;
          this.cargarDatosBarra();
        })
        .catch(() => {
          this.errorIniciales = true;
        });
    },
    cargarDatosBarra() {
      this.ebayCargado = false;
      this.olxCargado = false;
      this.errorEbay = false;
      this.errorOlx = false;
      fetch(
        "https://serverweb2.herokuapp.com/searchEbay?articulo=" +
          this.nombreProducto
      )
        .then((response) => response.json())
        .then((result) => {
          if (Object.keys(result).length !== 0) {
            this.datosBarras["ebay"] = [
              result.Maximo,
              result.Promedio,
              result.Minimo,
            ];
            this.datosAlternativas["ebay"] = result.otrosDatos;
            this.ebayCargado = true;
          } else {
            this.datosBarras["ebay"] = [0, 0, 0];
            this.errorEbay = true;
          }
          this.cambia = "" + Math.random();
        })
        .catch((e) => console.log("HUBO UN ERROR Ebay" + e));

      fetch(
        "https://serverweb2.herokuapp.com/searchOlx?articulo=" +
          this.nombreProducto
      )
        .then((response) => response.json())
        .then((result) => {
          if (Object.keys(result).length !== 0) {
            this.datosBarras["olx"] = [
              result.Maximo,
              result.Promedio,
              result.Minimo,
            ];
            this.datosAlternativas["olx"] = result.otrosDatos;
            this.olxCargado = true;
          } else {
            this.datosBarras["olx"] = [0, 0, 0];
            this.errorOlx = true;
          }
          this.cambia = "" + Math.random();
        })
        .catch((e) => console.log("HUBO UN ERROR olx" + e));
    },
  },
};
</script>