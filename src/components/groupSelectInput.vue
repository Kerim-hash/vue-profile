<template>
  <div class="group">
    <select class="group-select" v-model="selected">
      <option v-for="option in options" :key="option" :value="option.value">
        {{ option.text }}
      </option>
    </select>
    <Field
      class="group-input"
      v-maska
      :data-maska="selected"
      :value="phoneNumber"
      :name="name"
      type="text"
    />
  </div>
</template>

<script setup>
import { ref, watch } from "vue";
import { vMaska } from "maska";
import { Field } from "vee-validate";

import UploadFile from "../components/uploadAvatar.vue";
// props
const props = defineProps({
  name: {
    type: String,
    required: true,
  },
});
// select
const selected = ref("+1(###)###-####");
const rawValue = ref("");
const phoneValue = ref("");
const options = ref([
  { text: "🇺🇸", value: "+1(###)###-####" },
  { text: "🇰🇬", value: "+996(###)###-###" },
  { text: "🇷🇺", value: "+7(###)###-##-##" },
  { text: "🇦🇿", value: "+994-##-###-##-##" },
  { text: "🇰🇿 ", value: "+7(6##)###-##-##" },
]);

watch(selected, (value) => {
  phoneValue.value = rawValue.value;
});
</script>

<style lang="scss">
.group {
  display: flex;
  &-select {
    width: 70px;
    padding: 0 10px;
    border-radius: 5px 0 0 5px;
    border-right: 1px solid #ccc;
    cursor: pointer;
  }
  &-input {
    border-radius: 0 5px 5px 0;
  }
}
</style>
