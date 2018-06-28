<template>
     <div class='score'>
    <div class='card w-75 animated bounce text-center py-4 px-5 mb-3 mx-auto'>
    <h3 >Ranking</h3>
    <div class='container mb-4 px-5'>
     <div class='d-flex justify-content-between mb-4'>
      <span class='bits'>Username</span>
      <span class='bits text-right'>Score</span>
      <span class='bits text-right'>Date Played</span>
     </div>
     <div class='d-flex justify-content-between bits' v-for='user in
score'>
      <span>{{user.username}}</span>
      <span>{{user.score}}</span>
      <span>{{user.timestamp}}</span>
     </div>
    </div>
    <div class='w-100'>
      <router-link class='w-100 d-flex justify-content-center' to='/'>
       <button class='w-50 action-button animate green bits'>
        Back
       </button>
      </router-link>
    </div>
   </div>
  </div>
       
</template>
<script>
export default {
  data() {
    return {
      score: []
    };
  },
  created() {
    this.$http
      .get("https://vuejs-quiz-score.firebaseio.com/score.json")
      .then(function(data) {
        this.score = data.body;
        console.log(this.score);
      })
      .catch(function(data) {
        console.log("Error", data);
      });
  }
};
</script>
<style>
</style>
