<template>
  <div class="about">
    <div class="info">
      <div class="name">
          <h4>{{person.first_name}} {{person.last_name}}</h4>
          <p>"{{person.skill}}"</p>
      </div>
      <div class="avatar">
        <img :src="person.avatar" class="avatar-img">
      </div>
    </div>
    <div class="additional-information">
      <h3>Additional Information</h3>
      <ul class="stuff">
        <li>slogan: {{person.slogan}}</li>
        <li>birthplace: {{person.education}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      person: Object
    }
  }
</script>

<style>
  .about {
    background-color: rgba(255, 255, 255, 0.8);
    border: 1px solid rgba(0, 0, 0, 0.8);
    padding: 40px;
    font-size: 30px;
    text-align: center;
    width: 800px;
  }
  .stuff {
    list-style: none;
  }
</style>
