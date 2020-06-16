<template>
  <div class="question-box-container">
    <b-jumbotron>

      <template v-slot:lead>
        {{  decoder(currentQuestion.question) }}

        <div v-if="currentQuestion.image_source != ''">
          <img :src="currentQuestion.image_source" alt="">
        </div>
      </template>

      <hr class="my-4">


      <b-list-group>
     
          <b-list-group-item  v-for="(answer, index) in answers" :key="index" 
          @click.prevent="selectAnswer(index)"
          :disabled="answered"
          :class="answerClass(index)"
          >

          {{ answer }}
          </b-list-group-item>
       
      </b-list-group>

      <b-button 
        variant="primary"
        @click="submitAnswer"
        :disabled="selectedIndex === null || answered"
        >
        Vastaa

      </b-button>
      <b-button @click="next" :disabled="!answered" variant="success">
        Seuraava
      </b-button>
    </b-jumbotron>
  </div>
</template>

<script>
import _ from 'lodash'
export default {
  props : {
    currentQuestion: Object,
    next: Function,
    increment: Function
  },
  data () {
    return {
      selectedIndex: null,
      correctIndex: null,
      shuffledAnswers: [],
      answered: false
    }
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers]
      answers.push(this.currentQuestion.correct_answer)
      return this.shuffledAnswers
    }
  },
  watch: {
    currentQuestion: {
     immediate: true,
     handler() {
        this.selectedIndex = null
        this.shuffleAnswers()
        this.answered = false
     }
    }
  },
  methods: {
      selectAnswer(index) {
        this.selectedIndex = index
      },
      shuffleAnswers() {
        let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
        this.shuffledAnswers = _.shuffle(answers)
        this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
      },
      submitAnswer() {
        let isCorrect = false
        if(this.selectedIndex === this.correctIndex) {
          isCorrect = true
        }

        this.increment(isCorrect)

        this.answered = true
      },
      answerClass(index) {
        let answerClass = ''
        
        if(!this.answered && this.selectedIndex === index) {
          answerClass = 'selected'
        } else if(this.answered && this.correctIndex === index) {
          answerClass = 'correct'
        } else if(this.answered && this.selectedIndex === index && this.correctIndex !== index) {
          answerClass = 'incorrect'
        }

        return answerClass
      },
     decoder(str) {
       let textArea = document.createElement('textarea')
       textArea.innerHTML = str
       return textArea.value
     }
  }
}
</script>


<style scoped>
  .list-group {
    margin-bottom: 15px;
  }

  .list-group-item:hover {
    background: #eeeeee;
    cursor: pointer;
  }

  .btn {
    margin: 0 5px;
  }

  .selected {
    background-color: lightblue;
  }

  .correct {
    background-color: lightgreen;
  }

  .incorrect {
    background-color: red;
  }

</style>