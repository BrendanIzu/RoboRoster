<template>
<div class="wrapper">
  <div class="persons">
    <div class="person" :class="{ 'on-roster': onRoster}" v-for="person in persons" :key="person.id">
      <div class="info">
        <div class="name">
            <h4>{{person.first_name}} {{person.last_name}}</h4>
        </div>
        <div class="avatar">
          <img :src="person.avatar" class="avatar-img">
        </div>
      </div>
      <div class="skill">
        <p>"{{person.skill}}"</p>
      </div>
      <div class="add-btn-container" v-if="notOnRoster(person)">
        <button class="recruit" v-bind:class="{out:fullRoster()}" @click="addPerson(person)">
          Recruit
        </button>
      </div>
      <div class="on-roster" v-else>
        <button class="remove" @click="removeMember(person)">Remove</button>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  props: {
    persons: Array
  },
  methods: {
    addPerson: function(person) {
      const roster = this.$root.$data.roster;
      if(roster.length >= 5) {
        alert("max amount of members on roster is 5");
        return;
      }
      if(roster.includes(person)) {
        alert("This person is already on your roster")
      }
      else roster.push(person);
    },
    notOnRoster: function(person) {
      if(this.$root.$data.roster.includes(person)) {
        return false;
      }
      else return true;
    },
    removeMember: function(person) {
      const roster = this.$root.$data.roster;
      const index = roster.indexOf(person);
      roster.splice(index,1);
    },
    fullRoster: function() {
      if(this.$root.$data.roster.length == 5) {
        return true;
      }
      else {
        return false;
      }
    }
  }
}
</script>

<style>
  .persons {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    background-color: white;
    padding: 10px;
    grid-gap: 10px;
  }
  .person {
    background-color: rgba(255, 255, 255, 0.8);
    border: 1px solid rgba(0, 0, 0, 0.8);
    padding: 40px;
    font-size: 30px;
    text-align: center;
  }
  .info {
    display: flex;
    justify-content: space-between;
  }
  .avatar {
    background-color: white;
    height: 90px;
    width: 90px;
    display: flex;
    border: solid black;
  }
  .on-roster{
    color: red;
  }
  .recruit {
    background-color: #4CAF50; /* Green */
    border: none;
    color: white;
    padding: 16px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    transition-duration: 0.4s;
    cursor: pointer;
  }
  .remove {
    background-color: red; /* Green */
    border: none;
    color: white;
    padding: 16px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    transition-duration: 0.4s;
    cursor: pointer;
  }
  .out {
    opacity: 0.6;
    cursor: not-allowed;
  }

</style>
