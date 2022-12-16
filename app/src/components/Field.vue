<script setup>
defineProps(["modelValue", "as"]);
</script>

<template>
  <component
    :is="as"
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
  ></component>
</template>

<style scoped></style>
