<template>
  <div class="alert alert-success">
    <div class="results m-3">
      <h3>Correct: {{success}}</h3>
      <h3>Wrong: {{errors}}</h3>
    </div>
    <div class="buttons m-3">
      <button class="btn btn-primary" @click="$emit('again')">Try again</button>
      <button class="btn btn-primary" @click="$emit('next')">Continue</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ['success', 'errors']
}
</script>

<style>

</style>
