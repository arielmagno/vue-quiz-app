<template>
    <div class="results">
        <doughnut></doughnut>
        <div class="container">
      
        <div class="container">
            <router-link to ="/import">
              <button class="btn-primary">Upload Score</button>
            </router-link>

            <router-link to="/">
            <button class="btn-primary">Home Page</button>
            </router-link>
        </div>
        </div>
    </div>
</template>
<script>
import Doughnut from "./Doughnut";
export default {
  name: 'results',
  data() {
    return {
        
    };
  }, 
  components:{
    "doughnut": Doughnut
  }, 
  methods:{
    print: function(){
        console.log("Results");
    }
  }
};
</script>

<style>
</style>
