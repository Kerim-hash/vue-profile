<template>
  <Field
    class="select"
    :name="name"
    as="select"
  >
    <option v-for="option in options" :key="option" :value="option.text">
      {{ option.text }}
    </option>
  </Field>
</template>

<script setup>
import { ref } from "vue";
import { Field } from "vee-validate";
// state options
const options = ref([
  { text: "Chinese" },
  { text: "Arabic" },
  { text: "English" },
  { text: "Spanish" },
  { text: "Korean" },
  { text: "Russia" },
]);
// props
const props = defineProps({
  name: {
    type: String,
    required: true,
  },
});

</script>

<style></style>
