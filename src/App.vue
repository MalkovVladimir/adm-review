<template>
  <div>
    <Todo />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Todo from './components/todo.vue';

export default defineComponent({
  components: {
    Todo
  }
});
</script>
