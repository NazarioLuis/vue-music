<template>
  <div class="row">
    <Header titulo="Canciones favoritas" icono="favorite"/>
    <ListaCanciones :canciones="canciones"/>
  </div>
</template>
<script>
  import Header from '@/components/headers/Header.vue'
  import ListaCanciones  from '@/components/listas/ListaCanciones.vue'
  export default{
    name:'Favoritos',
    data(){
      return {
        canciones: [],
      }
    },
    components: {
      Header,ListaCanciones
    },
    mounted() {
      if (localStorage.favoritos){
         this.canciones = JSON.parse(localStorage.favoritos);
       }
    }
  }
</script>
