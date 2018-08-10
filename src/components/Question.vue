<template>
  <div class="alert bg-light text-center">
    <h2 class="m-3">{{x}} + {{y}} = ?</h2>
    <button v-for="answer in answers" @click="choose(answer)" class="btn btn-success m-3">{{answer}}</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      x: randNum(this.settings.from, this.settings.to),
      y: randNum(this.settings.from, this.settings.to),
    }
  },
  props: ['settings'],
  computed: {
    answers: function(){
      let res = [this.rightAnswer];
      while (res.length < this.settings.variants) {
        let num = randNum(this.rightAnswer - this.settings.range, this.rightAnswer + this.settings.range);
        if (res.indexOf(num) === -1){
          res.push(num);
        }
      }
      return res.sort(function() {
        return Math.random() > 0.5;
      });
    },
    rightAnswer: function(){
      return this.x + this.y;
    }
  },
  methods: {
    choose: function(answer){
      if(answer == this.rightAnswer){
        this.$emit('success');
      }
      else {
        this.$emit('error', `${this.x} + ${this.y} = ${this.rightAnswer}`);
      }
    }
  }
}
function randNum(min, max){
  let diff = max - min;
  return Math.floor((max - min + 1) * Math.random()) + min;
}
</script>

<style>

</style>
