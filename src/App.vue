<template>
  <div id="app">
    <Header 
    :numCorrect="numCorrect"
    :numTotal="numTotal"
    />

    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">

          <QuestionBox
            v-if="questions.length && index < 1"
            :currentQuestion="questions[index]"
            :next ="next"
            :increment="increment"
            :index="index"
           />

           <VideoContainer
           v-if="index >= 1"
           />
          
        </b-col>
      </b-row>
    </b-container>

  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'
import VideoContainer from './components/VideoContainer.vue'
export default {
  name: 'App',
  components: {
    Header,
    QuestionBox,
    VideoContainer
  },

  data() {
      return {
          questions : [],
          myQuestions: [],
          index: 0,
          numCorrect: 0,
          numTotal: 0
      }
  },
  methods: {
      next() {
          this.index++;
      },
      increment(isCorrect) {
          if(isCorrect) {
              this.numCorrect++
          }
          //this.numTotal++
      }
  },
  mounted: function() {
      /*fetch('https://opentdb.com/api.php?amount=10&category=21&type=multiple', {
          method: 'get'
      })
      .then((response) => {
          return response.json()
      })
      .then((jsonData) => {
          this.questions = jsonData.results
      })*/
      var question_1 = {correct_answer:"test", incorrect_answers: ["not test","real test","a test"],question:"what is the test type of test?", image_source: "https://i.pinimg.com/236x/cb/c8/7c/cbc87ce85795375cfbf2604e8fa725c2--cavalli-blue-cats.jpg" }

      this.questions.push(question_1)
      this.numTotal = this.questions.length
      
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
