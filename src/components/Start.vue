<template>
  <div class="start">
    <div class="mx-auto col-md-10">
  <div class="card" id="card-container">
    <div class="card-image">
      <a href="#">
        
        <img class="card-img-top img-fluid" id="bg-image" src="https://studentlife.lincolncollege.edu/wp-content/uploads/sites/42/2017/12/trivia-night-grpahic.png" alt="Card image cap">
      </a>
    </div>
    <div class="card-body mx-auto" >
      <h1 class="card-title">Are you ready to use your brain ?</h1>
      <p class="card-text text-danger">Click Start Game to begin.</p>
      
      <a href="#"  class="action-button animate w-400 custom-color my-2" @click="getQuestions()">Start Game</a>
       <router-link to = '/score'>
     <a href="#"  class="action-button animate w-400 custom-color my-2">View Leaderboard</a>
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
p{
  font-size:30px;
}
#bg-image{
  width: 100%;
  height:600px;
  
}

#card-container{
  border: groove 15px
}

.custom-color{
  background-color: #E2BC79;
}
</style>
