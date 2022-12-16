<script setup>
import { reactive, ref, watch } from "vue";

const errors = reactive({});

const isSubmitting = ref(false);

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
  isSubmitting.value = true;

  const validationErrors = props.validate(values);

  const hasError = Object.keys(validationErrors).length > 0;
  for (const key in validationErrors) {
    errors[key] = validationErrors[key];
  }

  if (!hasError) {
    emit(
      "submit",
      values,
      (submittingState) => (isSubmitting.value = submittingState)
    );
  } else {
    isSubmitting.value = false;
    setTimeout(() => {
      for (const key in validationErrors) {
        errors[key] = "";
      }
    }, 3000);
  }
}
</script>

<template>
  <slot
    :handleSubmit="handleSubmit"
    :values="values"
    :errors="errors"
    :isSubmitting="isSubmitting"
  >
  </slot>
</template>

<style scoped></style>
