<template>
    <div class="import">
    <div>
      <h3 class="bits" >Upload Score</h3>
      <div class="container">
        <label for="user">Your Score:</label>
        <label for="user" >{{upload.score}}</label>
        <label for="user">Enter your username:</label>
        <input type="text"  v-model="upload.username" >
        <button v-on:click="sendData()">Upload</button>
        <router-link to="results">
        <button >Back</button>
     </router-link>
    </div>
   </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      upload: {
        score: "",
        timestamp: new Date().toLocaleString()
      }
    };
  },
  methods: {
    sendData: function() {
      console.log(this.upload);
      this.$http
        .post("https://vuejs-quiz-score.firebaseio.com/score.json", this.upload)
        .then(function(data) {
          console.log(data);
          this.$router
            .push({
              name: 'start'
            })
            .catch(function(data) {
              console.log("Error", data);
            });
        });
    }
  },
  created() {
    this.upload.score = this.$store.getters.getScore;
  }
};
</script>
<style>
</style>
