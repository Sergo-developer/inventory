<script setup>
import { Skeleton } from '@brayamvalero/vue3-skeleton';
import '@brayamvalero/vue3-skeleton/dist/style.css';

const skeletonWidth = [155, 190, 170, 160, 140, 80];
</script>

<template>
  <div class="panel-wrapper">
    <div class="panel-image"></div>
    <div class="text-box">
      <div style="margin-top: 18px">
        <Skeleton
          width="190px"
          height="26px"
          background-color="#3c3c3c"
          border-radius="8px"
          inline
        />
      </div>
      <div style="margin-top: 18px">
        <Skeleton
          v-for="(el, i) in skeletonWidth"
          :key="i"
          :width="el"
          height="10px"
          background-color="#3c3c3c"
          border-radius="4px"
        />
      </div>
    </div>
  </div>
</template>

<style scoped>

.panel-wrapper {
  display: flex;
  flex-flow: column;
  justify-content: flex-start;
  align-items: center;
  width: 236px;
  height: 500px;
  border-radius: 12px;
  background-color: #262626;
  border: 1px solid #4d4d4d;
}

.panel-image {
  margin-top: 18px;
  width: 208px;
  height: 240px;
  border-radius: 8px;
  background-image: url('/UI/placeholder.png');
}

.text-box {
  color: white;
  width: 100%;
}
</style>
