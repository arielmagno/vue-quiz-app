<template>
    <div class="results">
      <br><br><br> 
       <b-card class="card" border-variant="success"
            header=" "
            header-bg-variant="success"
            header-text-variant="white"
            header-text-size="50px"
            align="center" 
            style="margin: 0 auto; float:none; margin-bottom: 10px"> 
            <h1>Congratulations for completing the quiz!</h1>  
            <br><br><br> 
           <h1>Your Score</h1>
           <h1>{{this.corrects}}/10</h1>
           <br><br><br> 
        <div class="container fluid" id="content-center">
            <router-link to ="/import">
              <button class="action-button animate w-300 blue my-1 bits center">Upload Score</button>
            </router-link>

            <router-link to="/">
            <button  class="action-button animate w-300 blue my-1 bits center">Home Page</button>
            </router-link>
            
        </div>
      </b-card>
    </div>
</template>
<script>
export default {
  name: 'results',
  data() {
    return {
       incorrects: this.$store.state.results.incorrect_answers,
        corrects: this.$store.state.results.correct_answers
        
    };
  }, 
  
  methods:{
    print: function(){
        console.log("Results");
    }
  }
};
</script>

<style>
.card {
        margin: 0 auto; /* Added */
        float: none; /* Added */
        margin-bottom: 10px; /* Added */
}
#content-center{
  width: 80%;
  display:flex; 
  align-items:center;
  justify-content: center
}

</style>

