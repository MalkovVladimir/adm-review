<template>
  <div v-if="isShown" class="popup">
    <div class="popup__container">
      <div class="popup__header">
        <slot name="header" />
      </div>
      <div class="popup__body">
        <slot />
      </div>
      <div class="popup__footer">
        <slot name="footer" />
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { defineProps } from "vue";

defineProps<{
  isShown: Boolean;
}>();
</script>

<style scoped>
.popup {
  position: absolute;
  top: 0;
  left: 0;

  display: flex;
  align-items: center;
  justify-content: center;

  width: 100vw;
  height: 100vh;
  background-color: rgba(136, 136, 136, 0.5);
}

.popup__container {
  min-width: 250px;
  display: grid;
  gap: 1rem;
  padding: 1rem;
  background: white;
  color: gray;
  border-radius: 1rem;
}

.popup__header {
  font-size: 16px;
  font-weight: 700;
}
</style>
