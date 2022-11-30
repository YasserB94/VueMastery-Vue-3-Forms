<script setup>
import { reactive } from "vue";
import BaseInput from "../components/form/BaseInput.vue";
let event = reactive({
  title: "",
  description:""
});
const logEvent = () => {
  console.table(JSON.parse(JSON.stringify(event)));
};
</script>

<template>
  <section>
    <header>
      <h1>Vue 3 Forms</h1>
    </header>
    <main>
      <form @submit.prevent="logEvent" class="flex flex-col">
        <BaseInput  name="title" v-model="event.title" />
        <BaseInput name="description" v-model="event.description" />
      </form>
    </main>
    <footer>Hi Mom!</footer>
  </section>
</template>

