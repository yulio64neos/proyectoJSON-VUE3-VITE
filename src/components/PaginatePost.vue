<template>
  <div class="btn-group" role="group" aria-label="Basic example">
    <button type="button" class="btn btn-outline-primary" @click="previus()" :disabled="inicio <= 0">
      Previus {{inicio}}
    </button>
    <button type="button" class="btn btn-outline-primary" @click="next()" :disabled="fin >= maxLength">
      Next {{fin}}
    </button>
  </div>
</template>

<script setup>
defineProps({
  next: Function,
  previus: Function,
  inicio: Number,
  fin: Number,
  maxLength: Number
});
const emit = defineEmits(["next", "previus"]);
</script>

<style>
</style>