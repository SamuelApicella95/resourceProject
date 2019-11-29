<template>
  <div class="container-fluid">

    <!--<nav class="navbar navbar-dark bg-dark">
      <button class="navbar-brand" to="/home/hello">AppLogo</button>

      <div class="right-bar">
        <ul class="navbar-nav">
          <li type="button" class="btn btn-cyan waves-effect waves-light"> Logout </li>
        </ul>
      </div>
    </nav>-->
    <nav class="navbar navbar-expand-md navbar-dark bg-dark shadow navbar-fixed-top">
      <router-link to="/home/hello" class="navbar-brand">AppNameHome</router-link>
      <button type="button" class="navbar-toggler" data-toggle="collapse" data-target="#navbarCollapse"><!--  what's use ??????????? -->
          <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarCollapse">
        <!--<div class="navbar-nav">
          <a href="#" class="nav-item nav-link active">Home</a>
          <a href="#" class="nav-item nav-link">About</a>
          <a href="#" class="nav-item nav-link">Products</a>
        </div>-->
        <form class="form-inline ml-auto">
          <input type="text" class="form-control mr-sm-2" placeholder="   fakeSearch">
          <button type="button" class="btn btn-outline-light" v-on:click="logout"><i class="material-icons">exit_to_app</i> Logout </button>
        </form>
      </div>
    </nav>



    <div class="row border-top">
      <ul class="col-md-1 sidebar-nav flex-column shadow">

          <!--<Tree :model="tree"/>-->
          <router-link class="btn btn-outline-dark btn-block rounded-0" to="/home/search">Search</router-link>
        <!--<div v-for="li in this.userPersMenu" v-bind:key=li>
          <router-link active-class="active" :to="li[0]">
            <h5>{{li[1]}}</h5>
          </router-link>
        </div>-->
      </ul>

      <main role="main" class="col">
        <router-view></router-view>
      </main>
    </div>
  </div>
</template>

<script>
//import Tree from './Tree'
export default {
  name: 'Home',
  /*components:{
    Tree
  },*/
  data: function () {
    return {
      username: this.$store.state.username,
      file: this.$store.state.file,
      userPersMenu:   [['/home/hello','Hello'],['/home/search','Search']],
      //tree:treeData
    }
  },
  mounted(){
    this.$router.push("/home/hello");
  },
  methods:{
    logout: function(){
      this.$store.state.auth=false;
      this.$router.push("/login");
    }
  }
}

/*var treeData = {
  name: 'Home', link: '/home/hello',
  children: [
    {name: 'Cerca', link: '/home/search', icon: 'search' }/*,
    {name: 'Risorsa', link: '/home/resource',
      children:[
        {name: 'Informazioni', link: '/home/info' },
        {name: 'Progetti', link: '/home/progetti' },
        {name: 'Esperienze', link: '/home/esperienze' }
      ]
    }       /
  ]
}*/
</script>


<style scoped>
  .col-md-1{
    background-color: #d6cbd3;
    padding-right:0px;
    padding-left:0px;
    display: inline-flex;
    justify-content: center;
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    z-index: 2;
  }
  .row{
    height: 100%;
    padding-top: 55px;
    margin-right: 0px;
  }
  .container-fluid{
    height:100%;
    padding-left: 0px;
    padding-right: 0px;
  }
  .col{
    padding-left: 10%;
  }
  .bg-light{
    height: auto;
  }
  .navbar{
    padding-left: 40px;
  }
  .nav-link {
    padding: 10px;
  }
  .navbar-nav{
    flex-direction: row;
  }
  .navbar-fixed-top{
    position: fixed;
    right: 0;
    left: 0;
    z-index: 1030;
  }
  .flex-column{
    /*padding-left: unset;*/
    margin-bottom: unset;
  }
  .btn{
    display: inline-flex;
  }
  .btn-outline-dark {
    border-color: transparent;
    background: darkgray;
    display: block;
  }
  .btn-outline-dark:hover{
    background:#1f202b;
    text-decoration-color: light;
  }
  .btn-outline-dark:focus{
    box-shadow: none;
    background: lightgrey;
  }
</style>