<script setup>
import { ref } from 'vue';
import { item } from '../stores/itemDatabase.js';
import Modal from './Modal.vue';

const slotsCount = new Array(25).fill(null);
const inventorySlots = ref(slotsCount);
const selectedItem = ref(null);

const clearSelected = () => {
  selectedItem.value = null;
};

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

inventorySlots.value[0] = item[0];
inventorySlots.value[1] = item[1];


const onDragOver = (event) => {
  event.preventDefault();
};

</script>

<template>
  <div class="inventory-wrapper">
    <div class="inventory">
      <div
          v-for="(slot, i) in inventorySlots"
          :key="i"
          :id="i"
          class="inventory-slot"
          @click="selectedItem = slot"
          @dragover="onDragOver"
          @drop="(event) => onDrop(event, i)"
      >
        <div
            v-if="slot"
            class="item"
            :style="{ backgroundImage: `url(${slot?.image})` }"
            draggable="true"
            @dragstart="(event) => onDragStart(event, i)"
        >
        </div>
        <div class="count-wrapper">
          <div v-if="slot?.count" class="count">{{ slot?.count }}</div>
        </div>
      </div>
    </div>
    <Modal v-if="selectedItem" :data="selectedItem" @childEvent="clearSelected"/>
  </div>
</template>

<style scoped>
.count {
  border-top: #4D4D4D solid 3px;
  border-left: #4D4D4D solid 3px;
  border-top-left-radius: 14px;
  min-width: 20px;
  color: white;
}

.count-wrapper {
  display: flex;
  justify-content: flex-end;
  align-items: flex-end;
  height: 99px;
  width: 105px;
}

.item {
  position: absolute;
  display: flex;
  background-repeat: no-repeat;
  background-size: 90px;
  height: 99px;
  width: 105px;
  cursor: pointer;
}

.inventory-slot {
  display: flex;
  justify-content: center;
  align-items: center;
  border-bottom: #4D4D4D solid 1px;
  border-right: #4D4D4D solid 1px;
  height: 99px;
  width: 105px;
}

.inventory-slot:nth-child(n + 21) {
  border-bottom: none;
}

.inventory-slot:nth-child(5n) {
  border-right: none;
}

.inventory {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  overflow: hidden;
  background-color: #262626;
}

.inventory-wrapper {
  position: relative;
  overflow: hidden;
  border: #4D4D4D solid 1px;
  border-radius: 12px;
}
</style>
