<template>
<div class="Search">
  <div class="container-fluid">
    <div class="col">
      <form class="d-flex align-items-center flex-column bd-highlight mb-3">
        <h4><span class="badge badge-pill badge-primary">Search</span></h4>
        <div class="input-group md-3">
          <span class="input-group-text" id="basic-addon1">Month</span>
          <input v-model="month">
        </div>
        <br>
        <div class="input-group md-3">
          <span class="input-group-text" id="basic-addon1">Year</span>
          <input v-model="year">
        </div>
        <br>
        <div class="input-group md-3">
          <span class="input-group-text" id="basic-addon1">Resource</span>
          <input v-model="resource">
        </div>
        <br>

        <button type="button" class="btn btn-primary" id="btn-search" v-on:click="Search"><i class="material-icons">search</i></button>

      <span class="badge badge-danger">{{error}}</span>
      </form>
    </div>

    <div v-if="showLoad">
      <span class="badge badge-pill badge-secondary">Loading ...</span>
    </div>
  </div>
</div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Search',
  data () {
    return {
      month: '2',
      year: '2019',
      resource: 'CALROS01002',
      showLoad: false,
      error:''
    }
  },
  methods: {
    Search: function () {
    this.$store.state.infoResource = '';
    this.error = '';
    this.dataArr = [];
    this.headArr = [];

    /*axios.post('http://192.168.6.132:8080/hrcont/api/v1/getCostiRisorsaPeriodo',
              { codiceRisorsa: this.resource, anno: this.year, periodo: this.month, tipoPeriodo: "C" })*/
    axios.get("./sample.json")
      .then( response => {
        this.$store.state.infoResource = response;
        this.showLoad = true;
      })
      .catch( error => {
        this.showLoad = false;
        this.error = error;
      })
      .then( () => {
        if(!(this.error === '')) return;
        this.showLoad = false;
        this.$router.push('/home/resource')
      })

    }

  }
}

</script>

<style scoped>
  .col {
    text-align: left
  }
  span#basic-addon1{
    width:100px;
  }
  .input-group{
    justify-content:center;
  }
  .badge-danger{
    margin-top: 20px
  }
  .Search {
    margin-top: 7%;
  }
  #btn-search {
    padding-bottom: unset;
  }
</style>
