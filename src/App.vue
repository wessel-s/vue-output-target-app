<script setup lang="ts">
import { onMounted, ref } from "vue";
import {
  GravityInput,
  GravityTextarea,
  GravitySelect,
  GravityCheckbox,
  GravityText,
} from "@gravity/web-components/src/wrappers/vue";

const inputRef = ref<any>(null);
const textareaRef = ref<any>(null);
const selectRef = ref<any>(null);
const checkboxRef = ref<any>(null);

const inputVModelValue = ref<string>("Initial Input Value");
const textareaVModelValue = ref<string>("Initial Textarea Value");
const selectVModelValue = ref<string[]>(["option1"]);
const checkboxVModelValue = ref<boolean>(false);

const selectOptions = [
  { id: "option1", label: "Option 1" },
  { id: "option2", label: "Option 2" },
];

onMounted(() => {
  inputRef.value?.$el.addEventListener("inputChanged", (event: CustomEvent) => {
    console.log("GravityInput Ref: inputChanged", event);
  });

  textareaRef.value?.$el.addEventListener(
    "inputChanged",
    (event: CustomEvent) => {
      console.log("GravityTextarea Ref: inputChanged", event);
    },
  );

  selectRef.value?.$el.addEventListener(
    "optionsSelected",
    (event: CustomEvent) => {
      console.log("GravitySelect Ref: optionsSelected", event);
    },
  );

  checkboxRef.value?.$el.addEventListener("changed", (event: CustomEvent) => {
    console.log("GravityCheckbox Ref: changed", event);
  });
});
</script>

<template>
  <div class="stack">
    <!-- GravityInput -->
    <GravityInput
      @input-changed="(e) => console.log('GravityInput @input-changed', e)"
      @inputChanged="(e) => console.log('GravityInput @inputChanged', e)"
      ref="inputRef"
      v-model="inputVModelValue"
    ></GravityInput>
    <GravityText
      >Value from v-model (Input): {{ inputVModelValue }}</GravityText
    >

    <!-- GravityTextarea -->
    <GravityTextarea
      @input-changed="(e) => console.log('GravityTextarea @input-changed', e)"
      @inputChanged="(e) => console.log('GravityTextarea @inputChanged', e)"
      ref="textareaRef"
      v-model="textareaVModelValue"
    ></GravityTextarea>
    <GravityText
      >Value from v-model (Textarea): {{ textareaVModelValue }}</GravityText
    >

    <!-- GravitySelect -->
    <GravitySelect
      :minWidth="false"
      :options="selectOptions"
      @options-selected="
        (e) => console.log('GravitySelect @options-selected', e)
      "
      @optionsSelected="(e) => console.log('GravitySelect @optionsSelected', e)"
      ref="selectRef"
      v-model="selectVModelValue"
    ></GravitySelect>
    <GravityText
      >Selected options (Select):
      {{ selectVModelValue.join(", ") }}</GravityText
    >

    <!-- GravityCheckbox -->
    <GravityCheckbox
      @changed="(e) => console.log('GravityCheckbox @changed', e)"
      label="Agree to Terms"
      ref="checkboxRef"
      v-model="checkboxVModelValue"
    ></GravityCheckbox>
    <GravityText>Checkbox Value: {{ checkboxVModelValue }}</GravityText>
  </div>
</template>

<style scoped>
.stack {
  display: grid;
  max-width: 500px;
}
.stack > :nth-child(odd):not(:first-child) {
  margin-top: 20px;
  margin-bottom: 5px;
}
</style>
