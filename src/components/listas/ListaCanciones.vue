<template>
  <div class="row">
    <Cancion v-for="cancion of canciones" :cancion="cancion" :album="(album||cancion.album)"
              :favorito="getFavorito(cancion)" @favoriteChange="favoriteChange" :key="cancion.id"/>
  </div>
</template>
<script>
  import Cancion from '@/components/cards/Cancion.vue'
  export default{
    name:'ListaCanciones',
    props: ['canciones','album'],
    data(){
      return {
        favoritos: [],
      }
    },
    components: {
      Cancion
    },
    methods: {
      favoriteChange(agregarFavorito,cancion){
        if(agregarFavorito) this.addFavorito(cancion);
        else this.removeFavorito(cancion);
      },
      getFavorito(cancion){
        return this.favoritos.find(favorito => favorito.id === cancion.id);
      },
      addFavorito(cancion) {
        this.favoritos.unshift(cancion)
        localStorage.favoritos = JSON.stringify(this.favoritos);
      },
      removeFavorito(cancion) {
        this.favoritos = this.favoritos.filter(favorito => favorito.id !== cancion.id);
        localStorage.favoritos = JSON.stringify(this.favoritos);
      },
    },
    mounted() {
      if (localStorage.favoritos){
         this.favoritos = JSON.parse(localStorage.favoritos);
       }
    }
  }
</script>
