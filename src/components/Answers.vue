<template>
    <div class='answers '>
  <div class='container ' >
    <p class="alert alert-success" style="display:inline-block" v-if="selected == correct && !gameActive">Congratulations! </p>
     <p  class="alert alert alert-danger" style="display:inline-block" v-if="selected != correct && !gameActive">Oops! Better luck next time. </p>
   <div class='row px-2' style="width: 100%;"  id="content-center">
  <br>
    <div v-for= 'option in options' >
     <div class='multiple-choice'>
      <button v-bind:class="{
        blue: gameActive, 
        disabled: !gameActive, 
        red: !gameActive, 
        yellow:selected == option && selected != correct, 
        green: !gameActive && selected == option && selected == correct || !gameActive && selected != correct && option == correct}"
         @click="pickOption(option)" 
         class="action-button animate w-300 blue my-1" >
       {{option}}
      </button>
     </div>
    </div>
   </div>
  </div>
  <br><br><br>
  <div class="content-center" style="display:inline-block">
     <button v-if='!gameActive' v-on:click='nextQuestion()' class='action-button animate blue w-100'>
       Next >
     </button>
    </div>
</div>
</template>
<script>
export default {
  props: ["answers"],
  data() {
    return {
      options: [],
      correct: "",
      gameActive: true,
      selected: "",
      status: false
    };
  },
  methods: {
    assign: function() {
      (this.options = this.answers.incorrect_answers),
        (this.correct = this.answers.correct_answer),
        (this.gameActive = true),
        (this.selected = "");
    },
    pickOption: function(a) {
      this.gameActive = false;
      this.selected = a;
      //check if the answer selected is correct
      if (this.correct == this.selected) this.status = true;
      else this.status = false;
    },
    // emits an event that the parent will listen and execute the nextQuestion
    nextQuestion: function() {
      console.log("Hola");
      //this.$emit('nextQuestion',this.status);
      this.$emit("nextQuestion", this.status);
      //console.log("Status" + this.status);
    }
  },
  created() {
    this.assign();
  },
  watch: {
    '$props': {
      handler: function(val, oldVal) {
        this.assign();
      },
      deep: true
    }
  }
};
</script>
<style>
#content-center{
  width: 100%;
  display:flex; 
  align-items:center;
  justify-content: center
}


</style>