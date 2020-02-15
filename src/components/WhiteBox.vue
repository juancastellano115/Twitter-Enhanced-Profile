<template>
  <div>
    <div class="titulo">
      <h2 class="mx-2 num rounded p-1">{{tweets}}</h2>
      <h4>Tweets en la última semana</h4>
    </div>
    <b-container class="d-flex justify-content-center">
      <div class="wrapperWhite">
        <h5 class="titlestats">Últimas menciones:</h5>
        <chart :chartdata="data" :options="options" />
      </div>
    </b-container>
  </div>
</template>

<script>
import chart from "@/components/chart.vue";
export default {
  props: {
    tweets: Number,
    text: String,
    data: Object,
    options: Object
  },
  components: {
    chart
  }
};
</script>

<style>
.wrapperWhite {
  text-align: center;
  padding: 1rem;
  color: rgb(37, 37, 37);
  border-radius: 0.25rem;
  max-width: 25em;
  background-color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
.titulo {
  color: rgb(224, 224, 224);
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  font-family: "Roboto", monospace;
  padding-bottom: 1em;
}
.num {
  background-color: rgb(247, 247, 247);
  color: rgb(24, 24, 24);
}
.titlestats {
  font-weight: 500;
  color: rgb(24, 24, 24);
  font-family: "Source Code Pro", monospace;
}
</style>