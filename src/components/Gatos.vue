<template>
  <div class="hello">
    <h1>Random Gif Cat</h1>
    <div>
      <form @submit.prevent='obtenerGif'>
        <div>
          <label>Titulo: </label>
          <input type="text" v-model="titulo">
        </div>
        <div>
          <label>Filtro: </label>
          <select v-model="filtro">
            <option>Blur</option>
            <option>Mono</option>
            <option>Sepia</option>
            <option>Negative</option>
            <option>Paint</option>
            <option>Pixel</option>
          </select>
        </div>
        <div>
          <label>Color: </label>
          <select v-model="color">
            <option value="blue">Azul</option>
            <option value="green">Verde</option>
            <option value="red">Rojo</option>
            <option value="yellow">Amarillo</option>
            <option value="grey">Gris</option>
            <option value="pink">Rosado</option>
          </select><span class="selecColor" :style="{backgroundColor: this.color}"></span>
            
        </div>
        <div>
          <label for="">Tamaño: </label>
          <input type="number" v-model="tamaño">
        </div>
        <button type="submit">Obtener Gif</button>
      </form>
    </div>
    <div class="gif">
      <img :src="this.imagen" alt="">
    </div>
  </div>
</template>

<script>
export default {
  name: 'Gatos',
  data() {
    return {
      titulo: '',
      filtro: '',
      color: '',
      tamaño: '',
      imagen: ''
    }
  },
  methods: {
    obtenerGif() {
      if(this.titulo && this.filtro && this.color && this.color && this.tamaño) {
        fetch(`https://cataas.com/cat/gif/says/${this.titulo}?filter=${this.filtro}&color=${this.color}&size=${this.tamaño}&type=or`)
        .then(result =>{
          console.log(result);
          this.imagen = result.url
        })
      }
    },
    created() {
      if(this.titulo && this.filtro && this.color && this.color && this.tamaño) {
        fetch(`https://cataas.com/cat/gif/says/${this.titulo}?filter=${this.filtro}&color=${this.color}&size=${this.tamaño}&type=or`)
        .then(result =>{
          console.log(result)
          this.imagen = result.url
        })
        .catch(error => console.log(error))
      }
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
body {
  margin: 0 !important;
  padding: 0 !important;
}
h1 {
  background-color: cadetblue;
  text-align: center;
  padding-top: 50px;
  padding-bottom: 50px;
  margin: 0;
}
form {
  display: block;
  background-color: pink;
  text-align: center;
  padding: 50px;
}
.selecColor {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  margin-left: 15px;
  display: inline-block;
}
select {
  padding: 5px;
  margin: 10px;
}
.gif {
  text-align: center;
  background-color: cadetblue;
  padding-top: 50px;
  padding-bottom: 200px;
}
button{
  margin-top: 5px;
}
</style>
