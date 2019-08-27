<template>
  <div class="col s3">
    <div class="card">
      <div class="card-image">
        <img v-bind:src="album.cover_medium">
         <router-link :to="{ name: 'DetalleAlbum', params: { id:album.id,album:album }}"
                      class="btn-floating halfway-fab waves-effect waves-light red">
           <i class="material-icons icon-red">queue_music</i>
         </router-link>
      </div>
      <div class="card-content">
        <span class="card-title">{{album.title}}</span>
        <p><strong>Artista: {{album.artist.name}}</strong></p>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name:'Album',
    props: {
      album: Object,
    }
  }
</script>

<style scoped>
  .card-content {
    height: 140px;
    line-height: normal;
    overflow-y: auto;
  }
  .card-title{
    font-size: 14pt !important;
  }
  i.icon-yellow {
    color: yellow;
  }
</style>
