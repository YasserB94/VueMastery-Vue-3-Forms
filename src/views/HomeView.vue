<script setup>
import { reactive } from "vue";
import BaseCheckbox from "../components/form/BaseCheckbox.vue";
import BaseInput from "../components/form/BaseInput.vue";
import BaseRadioGroup from "../components/form/BaseRadioGroup.vue";
import BaseSelect from "../components/form/BaseSelect.vue";
let event = reactive({
  title: "",
  description: "",
  category: "",
  catering: false,
  liveMusic: false,
  pets: "",
});
const petOptions = [
  { label: "Yes", value: 1 },
  { label: "No", value: "0" },
];
const logEvent = () => {
  console.table(JSON.parse(JSON.stringify(event)));
};
const categories = [
  "sustainability",
  "nature",
  "animal welfare",
  "housing",
  "education",
  "food",
  "community",
];
</script>

<template>
  <section>
    <header>
      <h1>Vue 3 Forms</h1>
    </header>
    <main>
      <form @submit.prevent="logEvent" class="my-20 space-y-2.5">
        <div class="form-item">
          <BaseInput name="title" v-model="event.title" />
        </div>
        <div class="form-item">
          <BaseInput name="description" v-model="event.description" />
        </div>
        <div class="form-item">
          <BaseSelect
            name="category"
            :options="categories"
            v-model="event.category"
          />
        </div>
        <div class="space-x-2">
          <BaseCheckbox name="catering" v-model="event.catering" />
          <BaseCheckbox name="live-music" v-model="event.liveMusic" />
        </div>
        <div >
          <BaseRadioGroup
            v-model="event.pets"
            name="pets"
            :options="petOptions"
          />
        </div>
        <div class="form-item"></div>
        <button type="submit">Say hi to mom</button>
      </form>
    </main>
    <footer>Hi Mom!</footer>
  </section>
</template>
<style scoped>
.form-item {
  @apply flex flex-col;
}
</style>
