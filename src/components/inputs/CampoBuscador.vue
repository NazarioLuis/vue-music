<template>
  <div class="row">
    <form class="col s12" @submit.prevent="actualizarFiltro">
      <div class="row">
        <div class="input-field col s12">
          <i class="material-icons prefix">search</i>
          <input :placeholder="placeholder" type="text" class="validate" v-model="filtro">
        </div>
      </div>
    </form>
  </div>
</template>

<script>
  export default {
    name:'CampoBuscador',
    data(){
      return {
        filtro: ''
      }
    },
    props: {
			placeholder: {
				type: String,
        default: 'Introducir un filtro de busqueda'
			}
		},
		methods: {
			actualizarFiltro() {
        this.$route.meta.filtro = this.filtro
				this.$emit('filtro', this.filtro);
			}
		},
    mounted() {
      this.filtro = this.$route.meta.filtro
      this.$emit('filtro', this.filtro);
    }
  }
</script>
