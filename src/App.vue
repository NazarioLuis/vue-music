<template>
  <div id="app" class="container">
    <router-view></router-view>
  </div>
</template>

<script>
  import router from '@/routes/index'

  export default {
    name: 'app',
    router,
    mounted() {
      M.AutoInit()
    }
  }
</script>
