<template lang=pug>
  #app
    img(src='./assets/logo.png')
    h1 LwMusic
    select(v-model="selectedCountry")
      option(v-for="country in countries" v-bind:value="country.value") {{ country.name }}
    spinner(v-show="loading")
    ul
      artist(v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid") {{ artist.name }}
</template>

<script>
import getArtists from './api'
import Spinner from './components/Spinner.vue'
import Artist from './components/Artist.vue'

export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries: [
      {name: 'Argentina', value: 'argentina'},
      {name: 'Colombia', value: 'colombia'},
      {name: 'España', value: 'spain'}
      ],
      selectedCountry: 'argentina',
      loading: true //la variable loading se utiliza como bandera para mostrar el spinner de carga de datos
    }
  },
  components: {
    Artist, //<-- Es el equivalente en JS2015 de Artist: Artist
    Spinner // Se creó un componente especial solo para el spinner de carga de datos
  },
  methods: {
    // Se creó la función refreshArtists para no duplicar código, pues éste método 
    // se llama al inicio de la carga de la página y cuando cambia la variable de estado
    // 'selectedCountry' por medio del combobox establecido para esa tarea.
    refreshArtists() {
      const self = this
      this.loading = true //mientras se hace la carga de datos, se debe mostrar el spinner
      this.artists = [] //durante la llamada a la API se resetea la lista de artistas
      getArtists(this.selectedCountry)
      .then(function(artists){
        self.loading = false  //cuando la llamada a la API finaliza se oculta el spinner
        self.artists = artists  //y se recarga la lista de artistas con los ítems que vienen de la API
      })
    }
  },
  mounted() {
    this.refreshArtists()
  },
  watch: {
    selectedCountry() {
      this.refreshArtists()
    }
  }
}
</script>

<style lang="stylus">
  #app 
    font-family 'Avenir', Helvetica, Arial, sans-serif
    -webkit-font-smoothing antialiased
    -moz-osx-font-smoothing grayscale
    text-align center
    color #2c3e50
    margin-top 60px
  h1, h2 
    font-weight normal
  ul 
    list-style-type none
    padding 0
  li 
    display inline-block
    margin 0 10px
  a 
    color #42b983
</style>
