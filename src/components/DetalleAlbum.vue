<template>
  <div class="row">
    <Header :titulo="'Album: '+mutableAlbum.title" icono="queue_music"/>
    <ListaCanciones :canciones="canciones" :album="mutableAlbum"/>
  </div>
</template>
<script>
  import Header from '@/components/headers/Header.vue'
  import ListaCanciones  from '@/components/listas/ListaCanciones.vue'
  export default{
    name:'DetalleAlbum',
    props: {
      id:{},
      album:{
        type:Object,
        default:function () {
          return {title:'',cover:null}
        }
      }
    },
    data(){
      return {
        canciones: [],
        mutableAlbum: JSON.parse(JSON.stringify(this.album)),
      }
    },
    components: {
      Header,ListaCanciones
    },
    mounted() {
      this.$http.get(`album/${this.id}/tracks`).then((response) => {
        this.canciones = response.data.data;
      })
      if (!this.mutableAlbum.title) {
        this.$http.get(`album/${this.id}`).then((response) => {
          this.mutableAlbum = response.data;
        })
      }
    }
  }
</script>
