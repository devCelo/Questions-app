<template>
  <div id="app">
    <Header />
    <b-container>
      <b-row>
        <b-col>
          <questionBox />
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
mounted: function() {
  fetch('https://opentdb.com/api.php?amount=10'), {
    method: "get"
  }
},
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
