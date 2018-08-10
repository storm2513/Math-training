<template>
  <div class="container">
    <h2 class="p-3 my-0">Math training. Level {{ level }}</h2>
    <div class="progress">
      <div class="progress-bar" :style="progressStyle"></div>
    </div>
    <transition name="flip" mode="out-in">
      <start v-if="currentComponent == 'start'"
             @onStart="onStart"></start>
      <question v-else-if="currentComponent == 'question'"
                @success="correct"
                @error="wrong"
                :settings="levels[level - 1]"></question>
      <message v-else-if="currentComponent == 'message'"
               :type="message.type"
               :text="message.text"
               @resume="resume"></message>
      <result v-else-if="currentComponent == 'result'"
              :success="stats.success"
              :errors="stats.errors"
              @again="again"
              @next="nextLevel"></result>
      <end v-else-if="currentComponent == 'end'"
           @newGame="newGame"></end>
    </transition>
  </div>
</template>

<script>
import Start from './components/StartScreen.vue'
import Question from './components/Question.vue'
import Message from './components/Message.vue'
import Result from './components/Result.vue'
import End from './components/End.vue'

export default {
  components: {
    Start: Start,
    Question: Question,
    Message: Message,
    Result: Result,
    End: End
  },
  data() {
    return {
      currentComponent: 'start',
      message: {
        type: '',
        text: ''
      },
      stats: {
        success: 0,
        errors: 0
      },
      maxQuestions: 10,
      level: 1,
      levels: [{
        from: 20,
        to: 40,
        range: 10,
        variants: 4
      },
      {
        from: 100,
        to: 200,
        range: 20,
        variants: 5
      },
      {
        from: 500,
        to: 1000,
        range: 40,
        variants: 6
      }]
    }
  },
  computed: {
    answersCount: function(){
      return this.stats.success + this.stats.errors;
    },
    progressStyle: function(){
      return { width: (this.answersCount / this.maxQuestions) * 100 + '%'}
    }
  },
  methods: {
    onStart: function(){
      this.currentComponent = 'question';
    },
    correct: function(){
      this.currentComponent = 'message';
      this.message.text = "Good job!";
      this.message.type = "success";
      this.stats.success += 1;
    },
    wrong: function(msg){
      this.currentComponent = 'message';
      this.message.text = 'Error! ' + msg;
      this.message.type = "warning";
      this.stats.errors += 1;
    },
    resume: function(){
      if (this.answersCount == this.maxQuestions){
        this.currentComponent = 'result';
      }
      else {
        this.onStart();
      }
    },
    nextLevel: function(){
      this.level++;
      if (this.level > this.levels.length){
        this.currentComponent = 'end';
        this.level = 'completed'
      }
      else{
        this.again();
      }
    },
    again: function(){
      this.stats.success = 0;
      this.stats.errors = 0;
      this.onStart();
    },
    newGame: function(){
      this.level = 1;
      this.again();
    }
  }
}
</script>

<style scoped>
.flip-enter-active {
  animation: flipInX 0.2s linear;
}

.flip-leave-active {
  animation: flipOutX 0.2s linear;
}

@keyframes flipInX {
  from{transform: rotateX(90deg);}
  to{transform: rotateX(0deg);}
}

@keyframes flipOutX {
  from{transform: rotateX(0deg);}
  to{transform: rotateX(90deg);}
}
</style>
