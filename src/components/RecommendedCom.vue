<template>
  <div class="wrapper">
    <div class="recommended">
      <div class="member" v-for="rec in recommended" :key="rec.id">
        <div class="add-card">
          <div class="avatar">
            <img :src="rec.avatar" class="avatar-img">
          </div>
          <div class="info">
            <div class="name">
              <h3>{{ rec.first_name }} {{ rec.last_name }}</h3>
            </div>
            <div class="skill">
              <button class="add" @click="addPerson(rec)">Add</button>
              <p>"{{rec.skill}}"</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      numRecs: Number
    },
    computed: {
      recommended() {
        const persons = this.$root.$data.persons;
        let randArray = [];
        let recommendedArray = [];
        for(let i=0; i<this.numRecs; i++) {
          let add = Math.floor(Math.random() * persons.length-1);
          while(randArray.includes(add)) {
            add = Math.floor(Math.random() * persons.length-1);
          }
          randArray.push(add);
        }
        for(let i=0; i<randArray.length; i++) {
          recommendedArray.push(persons[randArray[i]]);
        }
        return recommendedArray;
      }
    },
    methods: {
      addPerson: function(rec) {
        const roster = this.$root.$data.roster;
        if(roster.length >= 5) {
          alert("max amount of members on roster is 5");
        }
        else {
          roster.push(rec);
        }
      }
    }
  }
</script>

<style>
  .recommended {
    display: grid;
    grid-template-columns: repeat(autofit, minmax(500px, 1fr));
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
  .add {
    background-color: #4CAF50; /* Green */
    border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    cursor: pointer;
    }
</style>
