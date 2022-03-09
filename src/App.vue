<template>
  <div id="estilos">
    <h1 class="display-1">{{ encabezado }}</h1>
    <table class="table table-striped">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Fecha</th>
          <th scope="col">Estado</th>
          <th scope="col">Positivos/Negativos</th>
          <th scope="col">Pendiente resultado</th>
          <th scope="col">Hospitalizados</th>
          <th scope="col">Hopitalizados acumulado</th>
          <th scope="col">Con Ventilador</th>
        </tr>
      </thead>
      <tbody>
        <!-- puede ser of o in, i + 1 porque parte en o es un arreglo -->
        <tr v-for="(resultado, n1) of muestreocovid" :key="n1">
          <td>{{ 1 + n1 }}</td>
          <td>{{ resultado.date }}</td>
          <td>{{ resultado.states }}</td>
          <td>{{ resultado.positive }} / {{ resultado.negative }}</td>
          <td>{{ resultado.pending }}</td>
          <td>{{ resultado.hospitalizedCurrently }}</td>
          <td>{{ resultado.hospitalizedCumulative }}</td>
          <td>{{ resultado.onVentilatorCurrently }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  /* Van las variables */
  data() {
    return {
      encabezado: "Estadistica Covid 2021 US",
      muestreocovid: [],
    };
  },
  /* Funciones */
  created() {
    this.getData();
  },
  methods: {
    async getData() {
      try {
        const URL = "https://api.covidtracking.com/v1/us/daily.json"
        /* const request = fetch(URL);
        const data = await request.json(); */
        const request =await axios.get(URL)
        this.muestreocovid = request.data;
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>

<style>
#estilos {
  color: darkorchid;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
