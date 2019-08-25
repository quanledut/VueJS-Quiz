<template>
  <div class="question-box-container">
    <b-jumbotron  v-if="currentQuestion">
      <template slot="lead">
        {{ currentQuestion.question }}
      </template>

      <hr/>
      <b-list-group>
        <b-list-group-item v-for="(answer, index) in answers" :key="index" @click = 'selectAnswer(index)' :class="{ng_selected:selected==index}">
          {{answer}}
        </b-list-group-item>
      </b-list-group>
      <div>
        <b-button variant="primary" href="#" @click="prev">Prev</b-button>
        <b-button variant="success" href="#" @click="next">Next</b-button>
      </div>
      <b-button variant="secondary" href="#" @click="submit">Submit</b-button>
    </b-jumbotron>
  </div>
</template>
 
 <script>
  export default {
    props: {
      currentQuestion: Object,
      next: Function,
      prev: Function,
      submit: Function,
      selected: { type: Number, default: () => -1 },
      selectAnswer: Function
    },
    mounted() {
      console.log('mounted');
    },
    updated() {
      console.log('Updated');
    },
    watch: {
      selected(newVal, oldVal) {
        console.log('New' + newVal + 'old' + oldVal);
      }
    },
    computed: {
      answers() {
        return [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer];
      }
    },
    methods: {
      // selectAnswer(val) {
      //   this.$emit('change-selected', val)
      // }
    }
  }
 </script>

 <style scoped>
  .btn {
    margin: 15px 15px;
  }
  .list-group-item:hover {
    background-color: lightslategray;
  }
  .ng_selected {
    background-color: lightgreen;
  }
 </style>