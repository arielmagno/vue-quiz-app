<template>
    <div class='answers'>
      <div class="container">
        <div v-for = 'option in options'>
        <div class='multiple-choice'>
        <button v-bind:class='{
            blue:gameActive, 
            disabled: !gameActive, 
            yellow: selected == option && selected != correct,
            green: !gameActive && selected == option && selected == correct || 
            !gameActive && selected != correct && option == correct
        }' @click='pickOption(option)' >{{option}}</button>
        </div>
          </div>
          </div>
        <button v-if= '!gameActive' @click='nextQuestion' >Next</button>
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
    $props: {
      handler: function(val, oldVal) {
        this.assign();
      },
      deep: true
    }
  }
};
</script>
<style>
</style>
