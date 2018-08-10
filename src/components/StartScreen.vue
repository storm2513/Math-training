<template>
  <div class="alert alert-info text-center p-5">
    <h3 class="p-3">Are you ready to play?</h3>
    <button class="btn btn-success m-3" @click="$emit('onStart')">START</button>
  </div>
</template>

<script>
export default {
}
</script>

<style>

</style>
