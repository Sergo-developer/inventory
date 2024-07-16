<script setup>
const {} = defineProps({
  data: {}
})
const emit = defineEmits(['childEvent'])
const closeWindow = () => {
  emit('childEvent')

}
</script>

<template>
<div class="plate-wrapper">
  <div class="plate">
    <div class="close-button" ><div style="cursor: pointer" @click="closeWindow">x</div></div>
    <div class="item-image" :style="{ backgroundImage: `url(${data.image})` }"></div>
    <div class="item-name">{{ data.name }}</div>
    <div class="item-description">{{ data.description }}</div>
    <div class="delete">Удалить</div>
  </div>
</div>
</template>

<style scoped>
.delete {
  background-color: #FA7272;
  margin-top: 20px;
  width: 225px;
  border-radius: 14px;
  cursor: pointer;
}

.item-description {
  width: 225px;
  max-height: 360px;
  border-bottom: white solid 2px;
}

.item-name {
  font-size: 25px;
}

.close-button {
  display: flex;
  width: 220px;
  font-size: 25px;
  justify-content: flex-end
}

.item-image {
  background-repeat: no-repeat;
  background-size: 225px;
  height: 250px;
  width: 225px;
  border-bottom: white solid 2px;
}

.plate {
  display: flex;
  align-items: center;
  flex-direction: column;
  backdrop-filter: blur(10px);
  border-left: #4D4D4D solid 3px;
  height: 510px;
  width: 250px;
}

.plate-wrapper {
  animation: slide 0.2s;
  position: absolute;
  color: white;
  display: flex;
  justify-content: space-around;
  width: 250px;
  top: 0;
  right: 0;
  bottom: 0;
  transition: all 0.2s;
}

@keyframes slide {
  0% {
    right: -250px;
  }
  100% {
    right: 0;
  }
}
</style>
