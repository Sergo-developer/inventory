<script setup>
import { Skeleton } from '@brayamvalero/vue3-skeleton';
import '@brayamvalero/vue3-skeleton/dist/style.css';
</script>

<template>
  <div class="panel-wrapper">
    <Skeleton
      width="710px"
      height="41px"
      background-color="#3c3c3c"
      border-radius="16px"
      inline
    ></Skeleton>
    <div class="close-button">
      <div class="close-cross"></div>
    </div>
  </div>
</template>

<style scoped>
.panel-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 72px;
  border-radius: 12px;
  background-color: #262626;
  border: 1px solid #4d4d4d;
}

.close-cross {
  background-image: url('/public/UI/cross.png');
  background-size: 24px;
  height: 24px;
  width: 24px;
  cursor: pointer;
  top: 10px;
}

.close-button {
  position: absolute;
  display: flex;
  height: 72px;
  width: 41%;
  justify-content: flex-end;
}
</style>
