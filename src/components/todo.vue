<template>
  <div class="todo">
    <div class="todo__header">
      <input ref="search_input" type="text" class="todo-header__input">
      <button @click="addNewTodo">Add</button>
    </div>
    <div class="todo__body">
      <div v-for="value in items">
        <Item :value="value" @remove="remove" />
      </div>
    </div>
    <button class="todo__clear" @click="clear">Clear all</button>
  </div>
</template>

<script lang="ts">
import { defineComponent, Ref, ref } from 'vue';
import Item from './Item.vue';
import todoDefaultItems from '../default-items/todoDefaultItems'

export default defineComponent({
  setup() {
    var items: Ref<any[]> = ref(todoDefaultItems);
    const search_input = ref<HTMLInputElement | null>(null);
    const addNewTodo = () => {
      items.value.push({
        id: items.value.length,
        value: search_input.value?.value,
        is_done: false
      })
    }
    return {
      search_input,
      items,
      addNewTodo
    };
  },
  methods: {
    clear() {
      this.items = [];
    },
    remove(id: number) {
      delete this.items[id];
    }
  },
  components: { Item }
});
</script>

<style scoped>
.todo {
  display: grid;
  grid-template-rows: min-content 1fr min-content;
  height: 500px;
  width: 300px;
  padding: 1rem;
  border: 1px solid lightcyan;
  border-radius: 1rem;
}

.todo__header {
  display: flex;
  gap: 1rem;
}

.todo-header__input {
  width: 100%;
}

.todo__body {
  display: grid;
  grid-auto-rows: min-content;
  gap: 0.3rem;
  text-align: left;
  margin: 1rem 0;
}

.todo__clear:hover {
  background-color: crimson;
}
</style>