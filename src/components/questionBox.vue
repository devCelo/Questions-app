
<template>
  <div class="question-box-container">
    <b-jumbotron>
       <template slot="lead">
         {{ currentQuestion.question}}
       </template>

        <b-list-group>
          <b-list-group-item
          v-for="(answer, index) in answers"
          :key="index"
          @click="selectedAnswer(index)"
          :class="[selectedIndex === index ? 'selected' : '' ]"
          >

            {{ answer }}
          </b-list-group-item>
        </b-list-group>

       <b-button variant="primary" href="#">Submit</b-button>
       <b-button variant="success" href="#" @click="next" >Next</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
import _ from 'lodash'

export default {
  props: {
    currentQuestion: Object,
    next: Function
  },
  data() {
    return {
      selectedIndex: null,
      shuffledAnswers: []
    }
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers]
      answers.push(this.currentQuestion.correct_answer)
      return answers
    }
  },
  watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.selectedIndex = null
        this.shuffleAnswers()
      }
    }
  },
  methods: {
    selectedAnswer(index) {
      this.selectedIndex = index
    },
    shuffleAnswers() {
      let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
      this.shuffledAnswers = _.shuffle(answers)
    }
  }
}
</script>
