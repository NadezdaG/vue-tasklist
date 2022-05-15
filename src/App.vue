<script setup>
import { ref, computed } from "vue";
import Form from "./components/Form.vue";

const header = ref("Shopping List");
const items = ref([]);
const reversedItems = computed(() => [...items.value].reverse());
const editing = ref(false);

const saveItem = (item, priority) => {
  items.value.push({
    id: items.value.length + 1,
    label: item,
    priority: priority,
    purchased: false,
  });
};

const doEdit = (e) => {
  editing.value = e;
  /*newItem.value = "";
  newItemHighPriority.value = false;*/
};

const togglePurchased = (item) => {
  item.purchased = !item.purchased;
};
</script>

<template>
  <header>
    <h1>{{ header }}</h1>
    <button
      class="button button--secondary"
      v-if="editing"
      @click="doEdit(false)"
    >
      Cancel
    </button>
    <button class="button" v-else="editing" @click="doEdit(true)">Add</button>
  </header>
  <Form @submit="saveItem" v-if="editing" />
  <ul>
    <li
      v-for="(item, index) in reversedItems"
      :key="item.id"
      :class="{ strikeout: item.purchased, priority: item.priority }"
      @click="togglePurchased(item)"
    >
      {{ item.label }}
    </li>
  </ul>
  <p v-if="!items.length">Nothing added</p>
</template>

<style></style>

<style lang="scss">
@use "./assets/scss/variables.scss";
@use "./assets/scss/breakpoints.scss";
@use "./assets/scss/global.scss";

.taskList {
  background-color: var(--color-white);
  padding: 3em;
  width: 94%;
  max-width: 600px;
}

/*
@include breakpoints.min("medium") {
  .priority {
    color: green;
  }
}*/

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1em;
}

ul {
  li {
    background-color: var(--color-secondary-light);
    padding: 1em;
    margin-bottom: 1px;
    transition: background-color 0.5s;
    cursor: pointer;
    &:hover {
      background-color: var(--color-secondary);
      color: var(--color-white);
    }
    &.strikeout {
      text-decoration: line-through;
    }
    &.priority {
      font-weight: 800;
    }
  }
}
</style>
