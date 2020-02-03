<template>
  <div class="datos">

  <p>{{info}}</p>
  <p v-if="loading">Cargando...</p>
  </div>
</template>


<script>
export default {
  data(){
    return{
      info: null,
      loading: true,
      errored: false
    }
  }
  ,
  mounted () {
    this.axios
      .get('https://teprest.herokuapp.com/')
      .then(response => {
        this.info = response.data
      })
      .catch(error => {
        // eslint-disable-next-line no-console
        console.log(error)
        this.errored = true
      })
      .finally(() => this.loading = false)
  }
}
</script>