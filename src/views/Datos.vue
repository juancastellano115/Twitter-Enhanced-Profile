<template>
  <b-container class="datos">
    <b-container v-if="!loading">
      <b-container v-if="!errored">
        <b-img class="m-5 imagen" width="150" :src="foto" rounded="circle" />
        <h2 class="m-4 nombre">{{ nombre }}</h2>
        <h3 class="scrname">@{{ screen_name }}</h3>
         <h6 class="fecha"><i class="fa fa-calendar" aria-hidden="true"></i> {{ fecha }}</h6>
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
        <h5 class="desc m-5 d-flex rounded align-items-center justify-content-center">
          <i>{{ description }}</i>
        </h5>
        <WhiteBox :tweets="numero_tweets_ultima_semana" header="asdf" :data="chartdata" :options="options"/>
      </b-container>

      <b-container v-if="errored" class="center">
        <h3 class="scrname display-3">Oops! vaya vaya la papaia...</h3>
      </b-container>
    </b-container>
    <b-container class="center" v-if="loading">
      <b-spinner variant="primary" label="Spinning"></b-spinner>
    </b-container>
  </b-container>
</template>

<script>
import Darkcube from "@/components/DarkCube.vue";
import WhiteBox from "@/components/WhiteBox.vue";
import 'chartjs-plugin-colorschemes';
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
      fecha: null,
      numero_tweets_ultima_semana : null,
      mentions : null,
      loading: true,
      errored: false,
      chartdata: {
      labels: ['January', 'February','skere'],
      datasets: [
        {
          label: 'daata',
          data: [40, 20,23,23,45,74]
        }
      ]
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      plugins: {
            colorschemes: {
                scheme: 'brewer.Blues9'
            }
        }
      ,
      legend:{position:"right"}
    }
    };
  },
  components: {
    Darkcube,
    WhiteBox
  },
  mounted() {
    this.axios
      .get(`http://localhost:5000/${this.$route.params.userId}`)
      .then(response => {
        this.nombre = response.data.usuario.nombre;
        this.description = response.data.usuario.description;
        this.foto = response.data.usuario.foto;
        this.seguidores = response.data.usuario.seguidores;
        this.siguiendo = response.data.usuario.siguiendo;
        this.screen_name = response.data.usuario.screen_name;
        this.numero_tweets = response.data.usuario.numero_tweets;
        this.fecha = new Date(response.data.usuario.fecha).toLocaleString("ES-es",{ year: 'numeric', month: 'long', day: 'numeric' });
        this.numero_tweets_ultima_semana = response.data.estadisticas.tweetsSemana;
        this.mentions = response.data.estadisticas.menciones;
        
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
.fecha{
    font-family: "Source Code Pro", monospace;
    color: rgb(54, 141, 240);
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
.chartDisplay{
  font-family: "Source Code Pro", monospace;
  background-color: whitesmoke;
  color: rgb(37, 37, 37);
   
}
</style>
