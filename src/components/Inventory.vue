<script setup>
import { ref, watch, onMounted } from 'vue';
import { item } from '../stores/itemDatabase.js';
import Modal from './Modal.vue';

const slotsCount = new Array(25).fill(null);
const inventorySlots = ref(slotsCount);
const selectedItem = ref(null);
const selectedItemId = ref(null);
const dragImage = ref(null);

if (localStorage.getItem('inventory')) {
  inventorySlots.value = JSON.parse(localStorage.getItem('inventory'));
} else {
  inventorySlots.value[0] = item[0];
  inventorySlots.value[1] = item[1];
  inventorySlots.value[2] = item[2];
}

watch(inventorySlots.value, () => {
  localStorage.setItem('inventory', JSON.stringify(inventorySlots.value));
});

const deleteItems = (data) => {
  if (typeof data.value !== 'number' && selectedItem.value === null) {
    return;
  }

  const toDelete = Math.abs(data.value);
  if (selectedItem.value.count - toDelete <= 0) {
    inventorySlots.value[selectedItemId.value] = null;
  } else {
    inventorySlots.value[selectedItemId.value].count -= toDelete;
  }
};

const clearSelected = () => {
  selectedItem.value = null;
};

const onDragStart = (event, index) => {
  event.dataTransfer.effectAllowed = 'move';
  event.dataTransfer.setData('text/plain', index);
  dragImage.value.style.backgroundImage = `url('${inventorySlots.value[index].image}')`;
  event.dataTransfer.setDragImage(dragImage.value, 60, 60);
};

const onDrop = (event, index) => {
  const fromIndex = event.dataTransfer.getData('text/plain');
  const itemToMove = inventorySlots.value[fromIndex];
  inventorySlots.value[fromIndex] = inventorySlots.value[index];
  inventorySlots.value[index] = itemToMove;
};

const onDragOver = (event) => {
  dragImage.value.style.backgroundImage = `url('')`;
  event.preventDefault();
};

onMounted(() => {
  const ghostElement = document.createElement('div');
  ghostElement.style.position = 'absolute';
  ghostElement.style.top = '-9999px';
  ghostElement.style.left = '-9999px';
  ghostElement.style.width = '105px';
  ghostElement.style.height = '100px';
  ghostElement.style.backgroundSize = '54px';
  ghostElement.style.backgroundPosition = 'center';
  ghostElement.style.backgroundRepeat = 'no-repeat';
  ghostElement.style.backgroundColor = 'rgba(38,38,38,1)';
  ghostElement.style.border = '1px solid grey';
  ghostElement.style.borderRadius = '24px';
  document.body.appendChild(ghostElement);
  dragImage.value = ghostElement;
});
</script>

<template>
  <div class="inventory-wrapper">
    <div class="inventory">
      <div
        v-for="(slot, i) in inventorySlots"
        :key="i"
        :id="i"
        class="inventory-slot"
        @click="
          selectedItem = slot;
          selectedItemId = i;
        "
        @dragover="onDragOver"
        @drop="(event) => onDrop(event, i)"
      >
        <div
          v-if="slot"
          class="item"
          :style="{ backgroundImage: `url(${slot?.image})` }"
          draggable="true"
          @dragstart="(event) => onDragStart(event, i)"
        ></div>
        <div class="count-wrapper">
          <div v-if="slot?.count" class="count">{{ slot?.count }}</div>
        </div>
      </div>
    </div>
    <Transition>
    <Modal
      v-if="selectedItem"
      :data="selectedItem"
      @closeWindow="clearSelected"
      @deleteItems="deleteItems"
    />
    </Transition>
  </div>
</template>

<style scoped>

.v-enter-active,
.v-leave-active {
  transition: 0.2s;
}

.v-enter-from{
  right: -250px;
}
.v-leave-to{
  right: -250px;
}

.count {
  border-top: #4d4d4d solid 1px;
  border-left: #4d4d4d solid 1px;
  border-top-left-radius: 6px;
  width: 16px;
  height: 16px;
  font-size: 11px;
  color: #7d7d7d;
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
  background-size: 54px;
  height: 54px;
  width: 54px;
  cursor: pointer;
}

.inventory-slot {
  display: flex;
  justify-content: center;
  align-items: center;
  border-bottom: #4d4d4d solid 1px;
  border-right: #4d4d4d solid 1px;
  height: 100px;
  width: 105px;
}

.inventory-slot:hover {
  background-color: #2f2f2f;
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
  border: #4d4d4d solid 1px;
  border-radius: 12px;
  height: 500px;
}
</style>
