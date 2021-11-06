<template>
  <div class="person" v-if="this.$root.$data.roster.length==5">
    <h1 >About your team</h1>
    <div class="about-container">
      <button class="my-button" @click="cycle(-1)">
        <img src="../images/chevron-left.svg" alt="">
      </button>
      <AboutCom :person="person" :componentKey="componentKey"/>
      <button class="my-button" @click="cycle(+1)">
        <img src="../images/chevron-right.svg" alt="">
      </button>
    </div>
  </div>
  <div class="fill-message" v-else>
    <p>Navigate home or to roster page to finish filling up your roster</p>
  </div>
</template>

<script>
  import AboutCom from '../components/AboutCom.vue'
  export default {
    components: {
      AboutCom
    },
    data() {
      return {
        componentKey: 0
      }
    },
    computed: {
      person() {
        return this.$root.$data.roster[this.componentKey];
      }
    },
    methods: {
      cycle: function(interval) {
        if(interval > 0) {
          if(this.componentKey >= this.$root.$data.roster.length-1) {
            this.componentKey = 0;
          }
          else {
            this.componentKey += 1;
          }
        }
        else {
          if(this.componentKey <= 0) {
            this.componentKey = this.$root.$data.roster.length-1;
          }
          else {
            this.componentKey -= 1;
          }
        }
        console.log(this.componentKey);
      }
    }
  }
</script>

<style scoped>
  .about-container {
    display: flex;
    flex-direction: row;
    justify-content: center;
    padding: 30px;
  }
  .my-button {
    margin-top: 135px;
    margin-left: 15px;
    margin-right: 15px;
    width: 30px;
    height: 30px;
    border-radius: 100px;
    border: none;
    cursor: pointer;
  }
</style>
