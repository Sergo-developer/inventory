<script setup>
import Inventory from './components/Inventory.vue';
import LeftPanel from './components/LeftPanel.vue';
import BottomPanel from './components/BottomPanel.vue';
</script>

<template>
  <div class="app-wrapper">
    <div class="top-panels">
      <LeftPanel />
      <Inventory />
    </div>
    <BottomPanel />
  </div>
</template>

<style scoped>
.app-wrapper {
  display: flex;
  flex-direction: column;
  gap: 25px;
}

.top-panels {
  display: flex;
  gap: 25px;
}
</style>
