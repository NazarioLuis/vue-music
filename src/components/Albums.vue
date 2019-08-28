<template>
  <div class="row">
    <Header titulo="Buscador de Albums" icono="album"/>
    <CampoBuscador @filtro="recuperarPorFiltro"/>
    <Album v-for="album of albums" :album="album" :key="album.id"/>
  </div>
</template>

<script>
import Header from '@/components/headers/Header.vue'
import Album from '@/components/cards/Album.vue'
import CampoBuscador from '@/components/inputs/CampoBuscador.vue'

export default {
  name: 'Albums',
  data(){
    return {
      albums: []
    }
  },
  components: {
    Header,Album,CampoBuscador
  },
  methods: {
    recuperarPorFiltro(filtro) {
      this.$http.get('search/album',{
        params: {
          q: filtro,
          limit: 100
        }
      }).then((response) => {
        this.albums = response.data.data;
      })
    }
  },
}
</script>
