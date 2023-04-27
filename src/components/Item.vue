<template>
  <div v-if="value" :class="classList">
    <div class="todo-item__content">
      <input type="checkbox" :name="value.value" :id="value.id" v-model="value.is_done">
      <label>{{ value.value }}</label>
    </div>
    <button class="todo-item__remove" @click="$emit('remove', value.id)">X</button>
  </div>
</template>

<script>
import { computed } from '@vue/reactivity';
import { defineComponent } from 'vue';

export default defineComponent({
  props: {
    value: {
      type: Object,
      required: true,
    },
  },
  setup(props) {
    return {
      classList: computed(() => [
        'todo-item',
        props.value?.is_done ? 'todo-item__done' : ''
      ]),
    }
  }
});
</script>

<style scoped>
.todo-item {
  display: flex;
  justify-content: space-between;
  user-select: none;
  color: #888;
}

.todo-item__done .todo-item__content {
  text-decoration: line-through;
}

.todo-item__remove {
  display: flex;
  align-items: center;
  padding: 0 0.2rem;
  background-color: crimson;
  border-radius: 0.2rem;
}

.todo-item__remove {
  display: none;
}

.todo-item:hover .todo-item__remove {
  display: block;
  text-decoration: none;
}
</style>