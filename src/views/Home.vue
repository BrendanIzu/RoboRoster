<template>
  <div class="home">
    <h1 v-if="this.$root.$data.roster.length != 5">Add {{this.needed}} robots to your roster</h1>
    <h1 v-else>Your roster is complete!</h1>
    <PersonsCom :persons="persons"/>
    <footer>
      <a href="https://github.com/BrendanIzu/RoboRoster.git">github link</a>
    </footer>
  </div>
</template>

<script>
import PersonsCom from "../components/PersonsCom.vue"

export default {
  name: 'Home',
  components: {
    PersonsCom
  },
  data() {
    return {
    }
  },
  computed: {
    persons() {
      return this.$root.$data.persons;
    },
    needed() {
      return Math.abs(this.$root.$data.roster.length-5);
    }
  }
}
</script>
