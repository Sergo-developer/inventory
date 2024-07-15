<script setup>
import { ref } from 'vue';
import { item } from '../stores/itemDatabase.js';

const slotsCount = new Array(25).fill(null);
const inventorySlots = ref(slotsCount);

inventorySlots.value[0] = item[0]

const onDragStart = (event, index) => {
  event.dataTransfer.effectAllowed = 'move';
  event.dataTransfer.setData('text/plain', index);
};

const onDrop = (event, index) => {
  const fromIndex = event.dataTransfer.getData('text/plain');
  const itemToMove = inventorySlots.value[fromIndex];
  inventorySlots.value[fromIndex] = inventorySlots.value[index];
  inventorySlots.value[index] = itemToMove;
};

const onDragOver = (event) => {
  event.preventDefault();
};

</script>

<template>
  <div class="inventory-wrapper">
    <div
        v-for="(slot, i) in inventorySlots"
        :key="i"
        id="i"
        class="inventory-slot"
        @dragover="onDragOver"
        @drop="(event) => onDrop(event, i)"
    >
      <div
          class="item"
          :style="{ backgroundImage: `url(${slot?.image})` }"
          draggable="true"
          @dragstart="(event) => onDragStart(event, i)"
      >
      </div>
      <div class="count-wrapper" ><div v-if="slot?.count" class="count">{{slot?.count}}</div></div>
    </div>
  </div>
</template>

<style scoped>
.count{
  border-top: #1a1a1a solid 7px;
  border-left: #1a1a1a solid 7px;
  border-top-left-radius: 28px;
  color: white;
}

.count-wrapper {
  display: flex;
  justify-content: flex-end;
  align-items: flex-end;
  height: 150px;
  width: 150px;
}

.item{
  position: absolute;
  display: flex;
  background-repeat: no-repeat;
  background-size: 100px;
  height: 100px;
  width: 100px;
}

.inventory-wrapper{
  display: grid;
  grid-template-columns: repeat(5, 0fr);
  border-bottom: #1a1a1a solid 7px;
  border-right: #1a1a1a solid 7px;
}

.inventory-slot{
  display: flex;
  justify-content: center;
  align-items: center;
  border-top: #1a1a1a solid 7px;
  border-left: #1a1a1a solid 7px;
  height: 150px;
  width: 150px;
}
</style>
