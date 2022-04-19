<script setup>
defineProps(["title", "amount", "place"]);
</script>
<template>
  <div class="modal">
    <p>
      Товар <span class="bold">{{ title }}</span> в количестве
      <span class="bold">{{ amount }}</span> единиц добавлен в
      <span class="bold">{{ place }}</span>
    </p>
  </div>
</template>
<style lang="scss" scoped>
.modal {
  position: fixed;
  bottom: var(--normal);
  right: var(--normal);
  padding: var(--normal) var(--midi);
  background-color: var(--text);
  color: var(--bg);
  border: 1px solid var(--text);
  box-shadow: var(--bottom-line);
  z-index: 10;
  @media (max-width: 530px) {
    right: 0;
  }
}
.bold {
  font-weight: 600;
}
.js_fade {
  animation: fade 5s ease;
}
@keyframes fade {
  0% {
    opacity: 0;
  }
  15% {
    opacity: 1;
  }
  80% {
    opacity: 1;
  }
  100% {
    opacity: 0;
  }
}
</style>
