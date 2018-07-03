<template>
     <div class='score'>
         <br>
<div class="container fluid">
        
    <h1 class="text-center">Ranking</h1>
    <div class='container mb-4 px-5'>
     <table class="table table-hover"  >
         <tr class="table-primary text-center">
             <th><p>Rank</p></th>
            <th ><p>Username</p></th>
             <th><p>Score</p></th>
              <th><p>Date</p></th>
        </tr>
        <tbody>
        <tr v-for='(user, index) in score.slice(0,10)' class="table-success text-center"  >
             <td><p class="custom-font">{{index +1}}</p></td>
            <td><p class="custom-font">{{user.username}}</p></td>
            <td><p class="custom-font">{{user.score}}</p></td>
            <td><p class="custom-font">{{user.timestamp}}</p></td>
        </tr>
        </tbody>
        <br>
        
     </table>

    <div id="content-center">
<router-link to='/' >
       <button class="action-button animate w-300 blue my-1 bits center" id="content-center">
        Back
       </button>
      </router-link>
        </div>
        <br>
    
    
  </div>
</div>
</div>
       
</template>
<script>
export default {
  data() {
    return {
      rank: 0,
      score: [],
      items: [this.itemsArray]
    };
  },
  created() {
    this.$http
      .get("https://vuejs-quiz-score.firebaseio.com/score.json")
      .then(function(response) {
        console.log("Score" + response.data);

        //this.score= response.data;

        // for(let x in data.body){
        //     arr.push(data.body[x])}
        //     this.score = arr.sort((a, b => a.score < b.score ? 1: -1 ))
        //     console.log(this.score);

        // var temp = Object.values(response.data);
        // this.itemsArray = {

        //   username: temp.username,
        //   score: temp.score,
        //   timestamp: temp.timestamp

        // };
        let arr = [];
        for (let x in response.body) {
          arr.push(response.body[x]);
        }
        this.score = arr.sort((a, b) => (a.score < b.score ? 1 : -1));

        //return itemsArray;
      })

      .catch(function(response) {
        console.log("Error", data);
      });
  },

  
};
</script>
<style>
.custom-font{
    font-family: 'Calibri';
    font-size: 20px;
}
</style>
