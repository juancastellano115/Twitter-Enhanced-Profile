<template>
  <b-container class="datos">

    <b-container v-if="!loading">

      <b-container v-if="!errored">

        <b-img class="m-5 imagen" width="150" :src="foto" rounded="circle" />
        <h2 class="m-4 nombre">{{ nombre }}</h2>
        <h3 class="scrname">@{{ screen_name }}</h3>
        <b-row class="justify-content-center mt-3">
          <b-col md="2" sm="1">
            <Darkcube text="SEGUIDORES" :header="seguidores" />
          </b-col>
          <b-col md="2" sm="1">
            <Darkcube text="SIGUIENDO" :header="siguiendo" />
          </b-col>
          <b-col md="2" sm="1">
            <Darkcube text="TWEETS" :header="numero_tweets" />
          </b-col>
        </b-row>
        <h5
          class="desc m-5 d-flex rounded align-items-center justify-content-center"
        >
          <i> {{ description }}</i>
        </h5>
      </b-container>

      <b-container v-if="errored">
        <h3 class="scrname display-2">Oops! vaya vaya la papaia...</h3>
      </b-container>
      
    </b-container>
    <b-spinner v-if="loading" variant="primary" label="Spinning"></b-spinner>
  </b-container>
</template>

<script>
import Darkcube from "@/components/DarkCube.vue";
export default {
  data() {
    return {
      nombre: null,
      foto: null,
      description: null,
      seguidores: null,
      siguiendo: null,
      screen_name: null,
      numero_tweets: null,
      loading: true,
      errored: false
    };
  },
  components: {
    Darkcube
  },
  mounted() {
    this.axios
      .get(`http://192.168.1.55:5000/${this.$route.params.userId}`)
      .then(response => {
        this.nombre = response.data.nombre;
        this.description = response.data.description;
        this.foto = response.data.foto;
        this.seguidores = response.data.seguidores;
        this.siguiendo = response.data.siguiendo;
        this.screen_name = response.data.screen_name;
        this.numero_tweets = response.data.numero_tweets;
      })
      .catch(error => {
        // eslint-disable-next-line no-console
        console.log(error);
        this.errored = true;
      })
      .finally(() => {
        if (this.nombre == null && this.description == null) {
          this.errored = true;
        }
        this.loading = false;
      });
  }
};

//TODO cambiar las fuientes de google fonts y quitar roboto condensed
</script>

<style scoped>
.scrname {
  font-family: "Source Code Pro", monospace;
  color: rgb(0, 112, 243);
}
.desc {
  font-family: "Roboto", sans-serif;
  border: 0.5px rgb(192, 192, 192) solid;
  height: 3rem;
  padding: 2em;
}
.imagen {
  border: 0.5em rgb(0, 112, 243) solid;
}
</style>
