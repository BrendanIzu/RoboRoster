
<template>
  <div class="roster">
    <p v-if="isEmpty()">Your roster is currently empty, navigate to the Home page
    to make selections or choose from the recommendations below.</p>
    <div class="roster-header" v-else>
      <h1>Current Roster</h1>
      <p v-if="this.$root.$data.roster.length != 5">({{this.$root.$data.roster.length}}/5)</p>
    </div>
    <RosterCom :members="roster"/>
  </div>
</template>

<script>
import RosterCom from '../components/RosterCom.vue'

export default {
  components: {
    RosterCom
  },
  data() {
    return {
      roster: this.$root.$data.roster
    }
  },
  methods: {
    isEmpty: function() {
      if(this.$root.$data.roster.length == 0) return true;
      else return false;
    }
  }
}
</script>

<style scoped>
  .roster-header {
    display: flex;
  }
</style>
