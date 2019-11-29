<template>
<div class="Login">
  <form class="container">
    <div class="text-center">
      <h4><span class="badge badge-pill badge-warning">Login</span></h4>
      <div class="form-group">
        <div v-if="!errForm">
          <input type="username" class="form-control" placeholder="Username" v-model="username" required autofocus autocapitalize="off" spellcheck="false">
        </div>
        <div v-else>
          <input type="username" class="form-control is-invalid" placeholder="Username" v-model="username" autocapitalize="off" spellcheck="false">
        </div>
      </div>
      <div class="form-group">
        <div v-if="!errForm">
          <input type="password" class="form-control" placeholder="Password" v-model="password" autocapitalize="off" spellcheck="false">
        </div>
        <div v-else>
          <input type="password" class="form-control is-invalid" placeholder="Password" v-model="password" autocapitalize="off" spellcheck="false">
        </div>
        {{ password  }}
      </div>
      <button type="button" class="btn btn-primary" v-on:click="clickLogin">Login</button>
      <div class="alert alert-danger" role="alert" v-if="errForm">
        Username or password incorrect.
      </div>
    </div>
  </form>
</div>
</template>

<script>
export default {
  name: 'Login',
  data () {
    return {
      username: 'Sam',
      password: 'sam',
      errForm: false,
    }
  },
  methods: {
    clickLogin: function () {
      if (this.username === 'Sam' && this.$store.state.password === this.password) {
        this.$store.state.auth=true;
        this.$store.state.username = 'Sam';
        this.$router.push('/home');
      }else{
        this.errForm = true;
      }
    }
  },
  watch: {
    password:function(){
      this.errForm = false;
    },
    username:function(){
      this.errForm = false;
    }
  }
}
</script>

<style scoped>
  .container { 
    width: 22%;
    margin-top: 4%;
  }
  .alert {
    margin-top: 1rem;
    width: max-content;
    margin-left: auto;
    margin-right: auto;
  }
</style>