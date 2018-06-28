<template>
  <div class="start">
    <div class="mx-auto col-md-10">
  <div class="card">
    <div class="card-image">
      <a href="#">
        
        <img class="card-img-top img-fluid" src="https://snusercontent.global.ssl.fastly.net/listing-banner/4.jpg" alt="Card image cap">
      </a>
    </div>
    <div class="card-body mx-auto">
      <h5 class="card-title">Are you ready to be a millionaire?</h5>
      <p class="card-text text-danger">BEWARE: This game requires at least 2 million brain cells.</p>
      
      <a href="#" class="btn btn-lg btn-info bottom" @click="getQuestions()">Start Game</a>
       <router-link to = '/score'>
     <a href="#" class="btn btn-lg btn-info bottom">View Previous Millionaires</a>
      </router-link>
      <p class="card-text">
      </p>
    </div>
  </div>
</div>
   
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {};
  },
  methods: {
    //get the questions from our api
    getQuestions() {
      var router = this.$router;
      this.$store
        .dispatch("getQuestions")
        .then(function(data) {
          console.log("Successful");
          router.push({ name: "game" });
        })
        .catch(function(data) {
          console.log("Request rejected! ");
        });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
