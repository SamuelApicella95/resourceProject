<template>
  <div id = "Modal">
    <transition name="Modal">
      <div class="modal-mask">
        <div class="modal-wrapper">
          <div class="modal-container">

            <div class="modal-body">
              <slot name="body">
                <table class = "table">
                  <thead>
                    <tr>
                      <th scope="row" v-for="head in headArr" v-bind:key="head.id">{{ head }}</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr>
                      <td scope ="row">Retribuzioni</td>
                      <td v-for="data in this.$store.state.detailsRes" v-bind:key="data.id">{{data.retribuzioni}}</td>
                    </tr>
                    <tr>
                      <td scope ="row">Inail</td>
                      <td v-for="data in this.$store.state.detailsRes" v-bind:key="data.id">{{data.inail}}</td>
                    </tr>
                    <tr>
                      <td scope ="row">Contributivo</td>
                      <td v-for="data in this.$store.state.detailsRes" v-bind:key="data.id">{{data.contributivo}}</td>
                    </tr>
                    <tr>
                      <td scope ="row">Totale</td>
                      <td v-for="data in this.$store.state.detailsRes" v-bind:key="data.id">{{data.totale}}</td>
                    </tr>
                  </tbody>
                </table>
                <!--<button class="modal-default-button" @click="$emit('close')">
                  OK
                </button>-->
                <button type="button" class="modal-default-button btn btn-info" @click="$emit('close')">Ok</button>
              </slot>

            </div>

          </div>
        </div>
      </div>
    </transition>
  </div>
</template>


<script>

export default {
  name: 'Modal',
  data () {
    return {
      headArr: []
    }
  },
  mounted()  {
      this.headArr.push("");

      for(var i in this.$store.state.detailsRes){
        this.headArr.push(this.$store.state.detailsRes[i].tipoContributo);
      }

  }
}


</script>





<style scoped>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, .5);
  display: table;
  transition: opacity .3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 90%;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, .33);
  transition: all .3s ease;
  font-family: Helvetica, Arial, sans-serif;
}

.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

.modal-body {
  margin: 20px 0;
}

.modal-default-button {
  float: right;
}

/*
 * The following styles are auto-applied to elements with
 * transition="modal" when their visibility is toggled
 * by Vue.js.
 *
 * You can easily play with the modal transition by editing
 * these styles.
 */

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}

</style>