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
            v-if="questions.length && index < questions.length"
            :currentQuestion="questions[index]"
            :next ="next"
            :increment="increment"
            :index="index"
           />

           <VideoContainer
           v-if="index >= questions.length"
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
      var question_1 = {correct_answer:"Simon & Garfunkel - Bridge over Troubled Water", 
      incorrect_answers: ["Led Zeppelin - Led Zeppelin II","Alice Cooper - Pretties for You","The Rolling Stones - Sticky Fingers"],
      question:"Mikä albumi oli suomen albumilistan ykkönen vuonna 1970 kesäkuu/heinäkuu aikana?", 
      image_source: "" }


      var question_2 = {correct_answer:"2864", 
      incorrect_answers: ["5820","3644","1582"],
      question:"Mikä oli Saaren kunnan asukasluku vuonna 1970?", 
      image_source: "" }

      var question_3 = {correct_answer:"50", 
      incorrect_answers: ["230","7","25"],
      question:"Mikä on x:n arvo kun x on:", 
      image_source: "https://puu.sh/FWZdr/c15ab77f20.png" }

      this.questions.push(question_1)
      this.questions.push(question_2)
      this.questions.push(question_3)

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
