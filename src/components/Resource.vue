<template>
<div id="resource">
  <Modal v-if="showModal" @close="showModal = false"></Modal>

  <div class="btn-group btn-group-toggle" data-toggle="buttons">
    <label v-bind:class="{ 'btn btn-primary active': sel==='table' , 'btn btn-secondary': sel!=='table' }">
      <input type="radio" name="tabs" id="tab1" autocomplete="off" checked value="table" v-model="sel"> Costi
    </label>
    <label v-bind:class="{ 'btn btn-primary active': sel==='project' , 'btn btn-secondary': sel!=='project' }">
      <input type="radio" name="tabs" id="tab2" autocomplete="off" value="project" v-model="sel"> Progetti
    </label>
    <label v-bind:class="{ 'btn btn-primary active': sel==='exp' , 'btn btn-secondary': sel!=='exp' }">
      <input type="radio" name="tabs" id="tab3" autocomplete="off" value="exp" v-model="sel" > Esperienze
    </label>
  </div>

  <div v-show="sel === 'table'">

    <table class="table">
      <thead>
        <tr>
          <th scope="row" v-for="head in headArr" v-bind:key="head.id">{{ head }}</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td v-for="data in dataArr" v-bind:key="data.id">{{ data }}</td>
          <!-- chiamare funzione con click che formatta anche dati detailsRes prima di showModal-------------------------------------->
          <td><button type="button" class="btn btn-info" id="show-modal" @click="showModal = true">Dettagli</button></td>
        </tr>
      </tbody>
    </table>
    
  </div>
  <div v-show="sel === 'project'">
    Project
  </div>
  <div v-show="sel === 'exp'">
    Experience
  </div>

</div>
</template>

<script>
import Modal from './Modal'

export default {
  name: 'resource',
  components: {
    Modal
  },
  data(){
    return{
      infoResource: this.$store.state.infoResource,
      showModal: false,
      dataArr:[],
      headArr:[],
      sel:"table"
    }
  },
  mounted(){
    for(var i in this.infoResource.data.propertie){
      this.headArr.push(i);
    }

    for(var j in this.infoResource.data.propertie){
      this.dataArr.push(this.infoResource.data.propertie[j]);
    }

    this.$store.state.detailsRes = this.dataArr.pop();
  
  }
}
</script>