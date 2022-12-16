<script setup>
import { reactive } from "vue";

const errors = reactive({});

const props = defineProps({
  initialValues: {
    type: Object,
    required: true,
  },
  validate: {
    type: Function,
    required: true,
  },
});

const values = reactive({ ...props.initialValues });

const emit = defineEmits(["submit"]);

function handleSubmit() {
  const validationErrors = props.validate(values);

  for (const key in validationErrors) {
    errors[key] = validationErrors[key];
  }

  emit("submit", "test");
}
</script>

<template>
  <p>Form</p>
  <slot :handleSubmit="handleSubmit" :values="values" :errors="errors"> </slot>
</template>

<style scoped></style>
