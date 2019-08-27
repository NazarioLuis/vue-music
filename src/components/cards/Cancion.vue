<template>
  <div class="col s12">
    <div class="card horizontal">
      <div class="card-image">
        <img :src="album.cover">
      </div>
      <div class="card-content">
        <span class="card-title">{{cancion.title}}</span>
        <p><strong>Artista: {{cancion.artist.name}}</strong></p>
        <p><strong>Duración: {{duraccionEnMinutos(cancion.duration)}}</strong></p>
      </div>
      <div class="card-stacked">
        <div class="card-action">
          <a class="btn-floating green">
            <i :class="'material-icons'+(esFavorito?' yellow-icon':'')" @click="favoriteChange">favorite</i>
          </a>
          <router-link :to="{ name: 'DetalleCancion',
                        params: { id: cancion.id , album: album, cancion:cancion }}"
                        class="btn-floating blue">
            <i class="material-icons">play_circle_outline</i>
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name:'Cancion',
    props: ['cancion','album','favorito'],
    data(){
      return{
        esFavorito:(this.favorito!=null)
      }
    },
    methods: {
      duraccionEnMinutos(segundos) {
        var minutos = Math.floor(segundos / 60);
        segundos = segundos - minutos * 60;
        var pad = "00";
        segundos = (pad+segundos).slice(-pad.length);
        return `${minutos}:${segundos} min.`;
      },
      favoriteChange(){
        this.esFavorito = !this.esFavorito;
        this.cancion.album = this.album;
        this.$emit('favoriteChange', this.esFavorito, this.cancion);
      }
    }
  }
</script>

<style scoped>
  .card-content {
    line-height: normal;
    padding: 0px 25px !important;
  }
  .card-action{
    min-width: 150px;
  }
  .card-title{
    font-size: 14pt !important;
  }
  .card-action a{
    float: right;
    margin:  5px;
  }
  .yellow-icon{
    color: yellow;
  }
</style>
