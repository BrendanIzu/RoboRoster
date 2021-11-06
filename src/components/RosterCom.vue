<template>
<div class="wrapper">
  <div class="roster">
    <div class="member" v-for="member in members" :key="member.id">
      <div class="info">
        <div class="name">
            <h4>{{member.first_name}} {{member.last_name}}</h4>
        </div>
        <div class="avatar">
          <img :src="member.avatar" class="avatar-img">
        </div>
      </div>
      <div class="skill">
        <p>"{{member.skill}}"</p>
      </div>

      <div class="remove-button">
        <button class="remove" @click="removeMember(member)">Remove</button>
      </div>
    </div>
  </div>
  <footer>
    <div class="rec-header" v-if="hasRecs()">
      <div class="title">
        <h1>Recommended Additions</h1>
      </div>
      <button class="refresh" type="submit"  @click="refresh">
        <img src="../images/refresh.png" width="20" height="20" alt="submit" />
      </button>
    </div>
    <div class="about-message" v-else>
      <p>Your roster is now complete!  navigate to the About page to learn more
      about your members</p>
    </div>
    <RecommendedCom :numRecs="numRecs" :key="componentKey"/>
  </footer>
</div>
</template>

<script>
import RecommendedCom from '../components/RecommendedCom.vue'
export default {
  components: {
    RecommendedCom
  },
  props: {
    members: Array
  },
  computed: {
    numRecs() {
      return Math.abs(this.$root.$data.roster.length-5);
    }
  },
  data() {
    return {
      recommendedArray: [],
      componentKey: 0,
      hover: false
    }
  },
  methods: {
    refresh: function() {
      this.componentKey += 1;
    },
    hasRecs: function() {
      if(this.$root.$data.roster.length == 5) {
        return false;
      }
      else return true;
    },
    removeMember: function(member) {
      const roster = this.$root.$data.roster;
      const index = roster.indexOf(member);
      roster.splice(index,1);
    }
  }
}
</script>

<style scoped>
  .roster {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    background-color: white;
    padding: 10px;
    grid-gap: 10px;
  }
  .member {
    background-color: rgba(255, 255, 255, 0.8);
    border: 1px solid rgba(0, 0, 0, 0.8);
    padding: 40px;
    font-size: 30px;
    text-align: center;
  }
  .refresh {
    height: 40px;
    margin-left: 10px;
    margin-top: 25px;
  }
  .remove:hover {
    background: gray;
    height: auto;
  }
  .right {
    display: grid;
  }
  .member {
    display: grid;
  }
  .rec-header {
    display: flex;
    justify-content: center;
  }
</style>
