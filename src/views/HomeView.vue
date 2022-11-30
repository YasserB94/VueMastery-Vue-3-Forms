<script setup>
import { reactive } from "vue";
import axios from "axios";

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
const sendForm = async () => {
  //Run with command : npm run mockserver
  const MOCK_JSON_SERVER_ENDPOINT_URL = "http://localhost:5174/events";
  logEvent();
  try {
    const response = await axios.post(MOCK_JSON_SERVER_ENDPOINT_URL, event);
    console.log(`Submitted form: ${response.status} : ${response.statusText}`);
  } catch (e) {
    console.warn("Something went wrong during form submit");
    console.table({ "Error Message": e.message, "Error Code": e.code });
    console.warn(`Make sure you run the mockserver`);
    console.log(`npm run mockserver from root directory`);
  }
};
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
      <form @submit.prevent="sendForm" class="my-20 space-y-2.5">
        <h1>Create an Event</h1>
        <fieldset>
          <legend>Name and describe your event</legend>
          <div class="form-item">
            <BaseInput
              name="title"
              id="event-form-title"
              v-model="event.title"
            />
          </div>
          <div class="form-item">
            <BaseInput
              name="description"
              id="event-form-description"
              v-model="event.description"
            />
          </div>
        </fieldset>

        <div class="form-item">
          <BaseSelect
            id="event-form-category"
            name="category"
            :options="categories"
            v-model="event.category"
          />
        </div>
        <div class="space-x-2">
          <BaseCheckbox
            name="catering"
            id="event-form-catering"
            v-model="event.catering"
          />
          <BaseCheckbox
            name="live-music"
            id="event-form-music"
            v-model="event.liveMusic"
          />
        </div>
        <div>
          <BaseRadioGroup
            v-model="event.pets"
            name="pets"
            id="event-form-pets"
            :options="petOptions"
          />
        </div>
        <div class="form-item"></div>
        <button type="submit" class="form-submit">Submit</button>
      </form>
    </main>
    <footer>Hi Mom!</footer>
  </section>
</template>
<style scoped>
.form-item {
  @apply flex flex-col;
}
.form-submit {
  @apply rounded-2xl border bg-gradient-to-tr from-white to-slate-400 p-2 shadow hover:bg-gradient-to-bl hover:shadow-inner;
}
</style>
