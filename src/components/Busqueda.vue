<template>
  <div class="hello">
    <b-container>
      <i class="fab fa-twitter fa-6x"></i>
      <h1>Twitter Enhanced Profile</h1>
      <b-container>
        <b-form-input
          class="border-0"
          v-model="user"
          placeholder="Enter your name"
          @change="onsumbit"
        ></b-form-input>
      </b-container>
    </b-container>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      user: ""
    };
  },
  methods: {
    onsumbit: function() {
      this.$router.push({ name: "datos", params: { userId: `${this.user}` } });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  margin: 3rem;
  color: white;
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

input {
  height: 4rem;
  font-size: 20pt;
  background: #212d3a;
  font-family: "Source Code Pro", monospace;
}
.form-control:focus {
  background: #212d3a;
  color: rgb(121, 184, 255);
}

.fa-twitter {
  color: rgb(0, 112, 243);
}
</style>
