<template>
  <div class="hello">
    <img src="../assets/LogoMakr_43piDa.png" alt="" id="logo">
    <h1 class="font-weight-bold">Twitter Enhanced Profile</h1>
    <b-container>
      <b-form-input class="border-0" v-model="user" placeholder="Enter your name" @change="onsumbit"></b-form-input>
    
    </b-container>

  </div>
</template>

<script>

export default {
  name: 'HelloWorld',
  data(){
    return{
      user : "",
    }
  }
  ,
    methods: {
     onsumbit : function () {
       this.$router.push('/Datos')
     }
   }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  margin: 3rem;
  color: #7386e4
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

input{
  height: 4rem;
  font-size: 20pt;
  background: #212d3a;

}
.form-control:focus {
        box-shadow: 0 0 0.8rem 0.2rem  rgba(96, 60, 255, 0.774);
        background: #212d3a;
        color: white;
    } 

#logo {
  width: 9rem;
  margin-top: 3rem;
}

</style>
