<template>
  <div class="home">
      <transition appear name="fade">
      <Busqueda/>
      </transition>
  </div>
</template>

<script>
// @ is an alias to /src
import Busqueda from '@/components/Busqueda.vue'

export default {
  name: 'home',
  components: {
    Busqueda
  }
}
</script>

<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity 1s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>