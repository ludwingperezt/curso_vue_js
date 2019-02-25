<template lang="pug">
    li
        h2: a(v-bind:href="artist.url" target="_blank") {{ artist.name }}
        img(:src="artist.image[2]['#text']")
</template>

<script>
export default {
    name: 'artist',
    props: ['artist']
}
</script>

<style lang="stylus" scoped>
    /*
        Con el atributo scope se evita que los estilos aplicados
        al componente sobreescriban estilos de otros componentes mediante
        la aplicación de data attributes a los elementos del entorno de las
        reglas CSS definidas.
    */
    li
        display block
        margin 10px 0
</style>