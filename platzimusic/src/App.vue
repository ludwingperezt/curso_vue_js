<template lang=pug>
  #app
    img(src='./assets/logo.png')
    h1 LwMusic
    ul
      artist(v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid") {{ artist.name }}
</template>

<script>
import getArtists from './api'
import Artist from './components/Artist.vue'

export default {
  name: 'app',
  data () {
    return {
      artists: []
    }
  },
  components: {
    Artist //<-- Es el equivalente en JS2015 de Artist: Artist
  },
  mounted: function (argument) {
    // body...
    const self = this
    getArtists()
      .then(function(artists){
        self.artists = artists
      })
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
