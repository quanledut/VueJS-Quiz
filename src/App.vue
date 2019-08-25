<template>
  <div id="app">
    <Header
      :total = 'questions.length'
      :currentIndex = 'index' 
    />
    <b-container>
      <b-row>
        <b-col sm = "3" lg="6" offset="3">
          <QuestionBox 
            :currentQuestion = "questions[index]"
            :next = "next"
            :prev = "prev"
            :change-selected = "changeSelected"
            :submit = 'submit'
            :selected = 'answers[index]'
            :selectAnswer = 'changeSelected'
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import QuestionBox from "./components/QuestionBox.vue";

export default {
  name: "app",
  components: {
    Header,
    QuestionBox
  },
  data() {
    return {
      questions: [],
      index:0,
      answers: [],
      // selected: null
    }
  },
  methods: {
    next(){
      this.index + 1 < 10 ? this.index++ : 10;
    },
    prev() {
      this.index > 0 ? this.index-- : 0
    },
    submit() {

    },
    changeSelected(answerIndex) {    
      // console.log(answerIndex);
      console.log(this.answers[this.index]);
      this.answers[this.index] == undefined ? this.answers.push(answerIndex) : this.answers[this.index] = answerIndex;
      console.log(this.answers[this.index]);
      this.$forceUpdate();

      // this.selected = answerIndex;
    }
  },
  mounted: function () {
      fetch('https://opentdb.com/api.php?amount=10&category=18&difficulty=easy', {
        method:'get'
        })
          .then(response => {
            return response.json();
          })
          .then(jsonData => this.questions = jsonData.results)
      }
    };
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
