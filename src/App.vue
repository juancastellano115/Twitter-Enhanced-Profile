<template>
  <div id="app">
    <div class="center">
    <router-view/>
    </div>
  </div>
</template>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: whitesmoke;
}

.center{
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    width: 100vw;
}


body { background: rgb(26, 30, 34) !important;}

</style>
