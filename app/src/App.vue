<script setup>
import Vuemik from "./components/Vuemik.vue";
import Field from "./components/Field.vue";

function validate(values) {
  const errors = {};
  if (values.username !== "toto") {
    errors.username = "Username doit contenir toto";
  }
  return errors;
}

function onSubmit(values, setSubmitting) {
  console.log("VALIDATION PASSED !!! ", values);

  setTimeout(() => {
    console.log(JSON.stringify(values, null, 2));
    setSubmitting(false);
  }, 400);
}
</script>

<template>
  <Vuemik
    :initialValues="{ username: 'johndoe', password: 'mypassword' }"
    :validate="validate"
    @submit="onSubmit"
  >
    <template v-slot="slotProps">
      <form @submit.prevent="slotProps.handleSubmit">
        <ul v-for="(v, k) in slotProps.errors" :key="k">
          <li>{{ v }}</li>
        </ul>
        <Field as="input" type="text" v-model="slotProps.values.username" />
        <Field as="input" type="password" v-model="slotProps.values.password" />
        <button type="submit" :disabled="slotProps.isSubmitting">Submit</button>
      </form>
    </template>
  </Vuemik>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}

.bg-red {
  background-color: red;
}
</style>
