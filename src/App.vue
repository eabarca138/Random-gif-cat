<template>
  <div id="app">
    <header class="py-5">
      <h1 class="m-0">Random Gif Cat</h1>
    </header>

  <form class="pb-5">

  <div>
    <label>Título:<input type="text" v-model="titulo"></label>
  </div>

  <div>
    <label>Filtro:<select v-model="filtro">
      <option v-for="f in filtros" :key="f">{{f}}</option>
    </select></label>
  </div>

  <div class="text-center">
    <label>Color:<select v-model="color" class="color">
      <option value="red">Rojo</option>
      <option value="white">Blanco</option>
      <option value="blue">Azul</option>
      <option value="green">Verde</option>
      <option value="yellow">Amarillo</option>
    </select></label> <span v-bind:style="{'background-color': color}" class="circulo"></span>
  </div>

  <div class="text-center">
    <label>Tamaño:<input v-model="tamaño" type="number" min="0" @keyup.enter="reqGato"/></label>
  </div>
  </form>

  <section>
      <button @click="reqGato" class="my-3">Obtener mi gatito</button>

      <div>
        <img v-show="show" :src="imagen" alt="MEOW!">
      </div>
  </section>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: "App",

  data() {
    return {
      filtros: ['blur', 'mono', 'sepia', 'negative', 'paint', 'pixel'],
      filtro: "",
      color: "",
      titulo: "",
      tamaño: "",
      imagen: "",
      show: false
    }
  },

  methods: {
    async reqGato() {
      const url = `https://cataas.com/cat/gif/says/${this.titulo}?filter=${this.filtro}&color=${this.color}&size=${this.tamaño}&type=or`
      try {
        const res = await axios(url)
        console.log(res);
        this.imagen = res.config.url;
        this.show = true
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
*{
  margin: 0;
}
header, section{
  background-color: #ADD8E6;
}
section{
  height: 100%;
}
form{
  background-color: #F08080;
}

label{
  display: inline-block;
}

.circulo{
  width: 1.875rem;
  height: 1.875rem;
  border: solid black 1px;
  border-radius: 50%;
  display: inline-block;
}
input, select{
  width: 12.5rem;
  margin-top: 3rem;
}
.color{
  width: 11rem;
}
</style>