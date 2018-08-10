<template>
  <div class="alert alert-success text-center">
    <h2 class="m-3">Congratulations! You completed math training!</h2>
    <button class="btn btn-success m-3" @click="$emit('newGame')">Train again</button>
  </div>
</template>

<script>
export default {
}
</script>

<style>

</style>
