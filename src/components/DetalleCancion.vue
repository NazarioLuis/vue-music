<template>
  <div class="row">
    <Header :titulo="datosCancion.title" icono="play_circle_outline"/>
    <Reproductor v-if="datosCancion.title" :cancion="datosCancion"/>
  </div>
</template>
<script>
import Header from '@/components/headers/Header.vue'
import Reproductor from '@/components/cards/Reproductor.vue'

export default {
  name: 'Cancion',
  props: {
    id:{},
    cancion:{
      type:Object,
      default:function () {
        return {title:''}
      }
    },
    album:{}},
  data(){
    return {
      datosCancion: Object.assign(this.cancion,{album:this.album})
    }
  },
  components: {
    Header,Reproductor
  },
  mounted() {
    if (this.cancion.title){
      this.$route.meta.breadCrumbs.album.to = `/album/${this.album.id}`;
    }
    else {
      this.$http.get(`track/${this.id}`).then((response) => {
        this.datosCancion = response.data;
        this.$route.meta.breadCrumbs.album.to = `/album/${this.datosCancion.album.id}`;
      })
    }
  }
}
</script>
