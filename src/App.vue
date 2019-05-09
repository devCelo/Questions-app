<template>
  <div id="app">
    <Header />
    <b-container>
      <b-row>
        <b-col>
          <questionBox
          :currentQuestion="questions[index]"
          :nextQuestion="next"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from './components/header.vue'
import questionBox from './components/questionBox.vue'

export default {
  name: 'app',
  components: {
    Header,
    questionBox
  },
  data() {
    return {
      questions: [],
      index: 0
    }
  },
  methods: {
    next() {
      this.index++
    }
  },
mounted: function() {
  fetch('https://opentdb.com/api.php?amount=15&difficulty=medium&type=multiple', {
    method: 'get'
  })
  .then((response) => {
  // eslint-disable-next-line
  return response.json()
  })
  .then((jsonData) => {
    this.questions = jsonData.results
  })
}
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
