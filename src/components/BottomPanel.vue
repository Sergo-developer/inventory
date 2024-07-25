<script setup>
import { Skeleton } from '@brayamvalero/vue3-skeleton';
import '@brayamvalero/vue3-skeleton/dist/style.css';
</script>

<template>
  <div class="panel-wrapper">
    <div style="margin-left: 18px">
      <Skeleton
        width="699px"
        height="36px"
        background-color="#3c3c3c"
        border-radius="12px"
        inline
      />
    </div>
    <div class="close-cross-wrapper">
      <div class="close-cross"></div>
    </div>
  </div>
</template>

<style scoped>
.panel-wrapper {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  height: 72px;
  border-radius: 12px;
  background-color: #262626;
  border: 1px solid #4d4d4d;
}

.close-cross {
  background-image: url('/UI/cross.png');
  background-size: 24px;
  height: 24px;
  width: 24px;
  cursor: pointer;
  margin-top: 8px;
  margin-right: 8px;
}

.close-cross-wrapper {
  display: flex;
  height: 72px;
  width: 100%;
  justify-content: flex-end;
}
</style>
