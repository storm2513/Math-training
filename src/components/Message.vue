<template>
  <div class="alert text-center" :class="'alert-' + type">
    <h2 class="m-3">{{text}}</h2>
    <hr>
    <button class="btn btn-primary m-3" @click="$emit('resume')">Continue</button>
  </div>
</template>

<script>
export default {
  props: ['type', 'text']
}
</script>

<style>

</style>
