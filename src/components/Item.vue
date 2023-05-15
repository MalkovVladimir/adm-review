<template>
  <div v-if="value" :class="classList">
    <div class="todo-item__content">
      <input type="checkbox" :name="value.value" :id="value.id" v-model="value.isDone">
      <label>{{ value.value }}</label>
    </div>
    <button class="todo-item__remove" @click="$emit('remove', value.id)">X</button>
  </div>
</template>

<script type="ts">
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
        props.value?.isDone ? 'todo-item__done' : ''
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
  display: none;
  align-items: center;
  padding: 0 0.2rem;
  background-color: crimson;
  border-radius: 0.2rem;
}

.todo-item:hover .todo-item__remove {
  display: flex;
  text-decoration: none;
}
</style>