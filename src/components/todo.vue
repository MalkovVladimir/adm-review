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
  <Popup :isShown="isPopupShown">
    <template #header>
      Helper
    </template>
    Do you need help?
    <template #footer>
      <div class="popup__actions">
        <button @click="closePopup">Yes</button>
        <button @click="closePopup">No</button>
      </div>
    </template>
  </Popup>
</template>

<script lang="ts">
import { defineComponent, Ref, ref, watch } from 'vue';
import Popup from './Popup.vue';
import Item from './Item.vue';
import todoDefaultItems from '../default-items/todoDefaultItems'

export default defineComponent({
  setup() {
    const items: Ref<any[]> = ref(todoDefaultItems);
    const search_input = ref<HTMLInputElement | null>(null);
    const addNewTodo = () => {
      items.value.push({
        id: items.value.length,
        value: search_input.value?.value,
        isDone: false
      })
    }
    const clear = () => {
      items.value = [];
    }
    const remove = (id: number) => {
      delete items.value[id];
    }

    const isPopupShown = ref(false);
    const lastClickDate = ref();
    window.addEventListener('click', () => {
      lastClickDate.value = Date.now();
    });

    let timeoutId: number;
    watch(lastClickDate, () => {
      if (timeoutId) {
        clearTimeout(timeoutId);
      }

      timeoutId = setTimeout(() => {
        if (lastClickDate.value && Date.now() - lastClickDate.value >= 60 * 1000) {
          isPopupShown.value = true;
        }
      }, 60 * 1000)
    })

    const closePopup = () => {
      isPopupShown.value = false;
    }

    return {
      search_input,
      items,
      isPopupShown,
      addNewTodo,
      clear,
      remove,
      closePopup
    };
  },
  components: { Item, Popup }
});
</script>

<style scoped>
.todo {
  display: grid;
  grid-template-rows: min-content 1fr min-content;
  height: 500px;
  width: 300px;
  padding: 1rem;
  border: 1px solid gray;
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

.popup__actions {
  display: flex;
  justify-content: space-around;
}
</style>