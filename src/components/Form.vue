<template>
  <form class="form" @submit.prevent="submitHandler">
    <input
      type="text"
      class="input"
      maxlength="100"
      v-model.trim="newItem"
      placeholder="Add an item"
    />

    <button class="button button--primary">Save</button>
    <label>
      <input type="checkbox" v-model="newItemHighPriority" />
      High Priority
    </label>
    <p class="counter">{{ characterCount }}/100</p>
  </form>
</template>

<script setup>
import { computed, ref } from "vue";

const characterCount = computed(() => {
  return newItem.value.length;
});
const newItem = ref("");
const newItemHighPriority = ref(false);

const emit = defineEmits(["submit"]);

function submitHandler() {
  emit("submit", newItem.value, newItemHighPriority.value);
  newItem.value = "";
  newItemHighPriority.value = false;
}
</script>

<style lang="scss">
@use "../assets/scss/breakpoints.scss";
@use "../assets/scss/global.scss";

.form {
  position: relative;
  padding: 1em;
  margin-bottom: 1em;
  background-color: var(--color-primary-light);
  display: flex;
  flex-wrap: wrap;
  justify-content: stretch;
  flex-basis: 50%;
  .counter {
    display: block;
    position: absolute;
    text-align: right;
    right: 0;
    bottom: 0;
    font-size: 0.6em;
    color: var(--color-white);
  }
  input.input {
    flex-grow: 3;
    background-color: var(--color-white);
    border-color: var(--color-white);
  }
  button {
    flex-grow: 1;
  }
  label {
    width: 100%;
    flex-grow: 1;
    display: flex;
    align-items: center;
    justify-content: flex-start;
    margin-top: 1em;
    font-size: 0.8em;
    cursor: pointer;
    color: var(--color-white);
  }
}
</style>
