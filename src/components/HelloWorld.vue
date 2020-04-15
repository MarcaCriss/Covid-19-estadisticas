<template>
  <div class="container py-5"><br><br>
    <h1 >Estadisticas Globales <span class="badge badge-primary">{{ getDate(datos.Date) }}</span></h1>
    <br><br>
    <h1>Confirmados</h1>
    <h2 v-for="dato in datos" :key="dato.key" class="">
      <b>{{ dato.TotalConfirmed }}</b>
    </h2>
    <br><br>
    <hr style="height: 5px; background: black">
    <br><br>
    <h1>Muertos</h1>
    <h2 v-for="dato in datos" :key="dato.key">
      <b>{{ dato.TotalDeaths }}</b>
    </h2>
    <br><br>
    <hr style="height: 5px; background: black">
    <br><br>
    <h1>Recuperados</h1>
    <h2 v-for="dato in datos" :key="dato.key">
      <b>{{ dato.TotalRecovered }}</b>
    </h2>
    <br><br>
    <h1>Estadisticas por Paises</h1>
    <br><br>
    <select class="custom-select" v-model="selected" @change="getPais()">
      <option :value="dato.Slug" v-for="dato in datos.Countries" :key="dato.key">{{ dato.Country }}</option>
    </select>
    <br><br>
    <div class="d-flex justify-content-center" v-for="datosPais in datosPaises" :key="datosPais.key">
      <div class="align-center centrado">
        <br><br>
        <h3>{{ getDate(datosPais.Date) }}</h3>
        <hr style="height: 1px; background: black; width: 405px">
        <br>
        <h1>
          <b>Confirmados</b>
        </h1>
        <hr style="height: 5px; width:250px; background: black">
          <h2>
            <b>{{datosPais.Confirmed}}</b>
          </h2>
        <br><br><br>
        <h1 >
          <b>Muertos</b>
        </h1>
        <hr style="height: 5px; width:200px; background: black">
        <h2>
          <b>{{ datosPais.Deaths }}</b>
        </h2>
        <br><br><br>
        <h1 >
          <b>Recuperados</b>
        </h1>
        <hr style="height: 5px; width:280px; background: black">
        <h2>
          <b>{{ datosPais.Recovered }}</b>
        </h2>
        <br><br>
        <hr style="height: 5px; width:auto; background: black">
      </div>
    </div>

  </div>
</template>

<script>

import axios from 'axios'
import Moment from 'moment';

export default {
  name: 'HelloWorld',
  data() {
    return {
      datos: [],
      selected: '',
      datosPaises:[]
    }
  },
  methods: {
    getDatos() {
      const path = "https://api.covid19api.com/summary";
      axios.get(path).then((response) => {
        this.datos = response.data;
      })
    },
    getDate(date) {
      Moment.locale('es');
      return Moment(date).format('D / MMMM / YYYY');
    },
    getPais() {
      const path = `https://api.covid19api.com/live/country/${this.selected}`;
      axios.get(path).then((response) => {
        this.datosPaises = response.data;        
      })
    }
  },
  created() {
    this.getDatos();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
option, select {
  font-size: 25px;
}
@media only screen and (max-width: 340px) and (min-width: 5px)  {
  .centrado {
    align-items: center
  }
}
</style>
