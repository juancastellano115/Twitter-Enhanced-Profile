<template>
 <transition appear name="fade">
  <b-container class="datos">
    <b-container v-if="!loading"> 
        <h2 class="m-4 nombre">{{nombre}}</h2>
        <b-img class="m-5" thumbnail fluid width="100" :src="foto" rounded="circle" />
        <div class="follow">
          <div class="seguidores"><b-badge variant="primary"><h5>Seguidores: {{seguidores}}</h5></b-badge> </div>
          <div class="siguiendo"><b-badge variant="primary"><h5>Siguiendo: {{siguiendo}}</h5></b-badge></div>
        </div>
         <h5 class="desc m-5 d-flex rounded align-items-center align-text-center">{{description}}</h5> 
       
    </b-container>
  </b-container>
 </transition>
</template>


<script>
export default {
  data() {
    return {
      nombre: null,
      foto: null,
      description: null,
      seguidores: null,
      siguiendo: null,
      loading: true,
      errored: false
    };
  },
  mounted() {
    this.axios
      .get(`http://localhost:5000/${this.$route.params.userId}`)
      .then(response => {
        this.nombre = response.data.nombre;
        this.description = response.data.description;
        this.foto = response.data.foto;
        this.seguidores = response.data.seguidores;
        this.siguiendo = response.data.siguiendo;
      })
      .catch(error => {
        // eslint-disable-next-line no-console
        console.log(error);
        this.errored = true;
      })
      .finally(() => (this.loading = false));
  }
};
</script>

<style scoped>
.nombre {
  font-family: 'Source Code Pro', monospace;
}
.desc{
  font-family: 'Roboto', sans-serif;
  border: 0.5px rgb(192, 192, 192) solid;
  height: 3rem;
  padding: 2em;
}
.follow div{
  display: inline;
  margin: 1em;
}
.fade-enter-active  {
  transition: opacity 3s;
}
.fade-leave-active{
transition: opacity 0s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>