<script setup>
defineProps(["name", "modelValue", "as", "type", "error"]);
</script>

<template>
  <div class="group">
    <span>{{name}} &nbsp;</span>
    <component :is="as" :type="type" :value="modelValue" @input="$emit('update:modelValue', $event.target.value)"></component>
    <p>{{ error }}</p>
  </div>
</template>

<style scoped>
  p {
    color: red;
  }

  span {
    text-transform: capitalize;
  }

  .group {
    display: flex;
    flex-direction: column;
    margin-bottom: 1rem;
    width: 40vw;
  }
</style>
