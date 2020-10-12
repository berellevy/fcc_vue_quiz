<template>
  <div class="quetion-box-container">
    <b-jumbotron>
      
      <template v-slot:lead>
        {{ currentQuestion.question }}
      </template>

      <hr class="my-4">

      <b-list-group>
        <b-list-group-item
          v-for="(answer, index) in answers"
          :key="index"
          @click="selectedAnswer(index)"
          :class="[selectedIndex === index ? 'selected' : '']"
        >
          {{ answer }}
        </b-list-group-item>
      </b-list-group>

      <b-button 
        variant="primary"
        @click="submitAnswer"
      >
        Submit
      </b-button>
      <b-button @click="next" variant="success" href="#">
        Next
      </b-button>
    </b-jumbotron>
  </div>
</template>

<script>
  import _ from 'lodash'
  export default {
    props: {
      currentQuestion: Object,
      next: Function,
    },
    data() {
      return {
        selectedIndex: null,
        shuffledAnswers: [],
      }
    },
    computed: {
      answers() {
        return [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
      },
    },
    watch: {
      currentQuestion: {
        immediate: true,
        handler() {
          this.selectedIndex = null
          this.shuffleAnswers()
        }
      },

    },
    methods: {
      selectedAnswer(index) {
        this.selectedIndex = index;
      },
      submitAnswer() {
        
      },
      shuffleAnswers() {
        let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
        this.shuffledAnswers = _.shuffle(answers)
      }
    },
  }
</script>

<style scoped>
  .list-group {
    margin-bottom: 15px;
  }
  .list-group-item:hover {
    background: #EEE;
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