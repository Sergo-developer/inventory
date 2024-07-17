<script setup>
import { ref } from 'vue';

const isDelete = ref(false);
const itemCountToDelete = ref(1);

const {} = defineProps({
  data: {}
});
const emit = defineEmits(['closeWindow', 'deleteItems']);
const closeWindow = () => {
  emit('closeWindow');
};
const deleteItems = () => {
  emit('deleteItems', itemCountToDelete);
  emit('closeWindow');
};
</script>

<template>
  <div class="plate-wrapper">
    <div class="plate">
      <div class="close-button">
        <div class="close-cross" @click="closeWindow"></div>
      </div>
      <div class="item-image-wrapper">
        <div class="item-image" :style="{ backgroundImage: `url(${data.image})` }"></div>
      </div>
      <div class="item-name">{{ data.name }}</div>
      <div class="item-description">{{ data.description }}</div>
      <div class="delete-window-button-wrapper" v-if="!isDelete">
        <div class="delete-window-button" @click="isDelete = true">Удалить</div>
      </div>
      <div class="delete-window" v-if="isDelete">
        <input class="item-to-delete-count-input" v-model="itemCountToDelete" :max="data.count"
               type="number">
        <div class="delete-buttons-wrapper">
          <div class="delete-button cancel" @click="isDelete = false">Отменить</div>
          <div class="delete-button confirm" @click="deleteItems">Подтвердить</div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.delete-button {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 33px;
  border-radius: 8px;
  cursor: pointer;
  box-shadow: #FA7272 0 0 20px;
}

.delete-button.confirm {
  background: #FA7272;
  width: 112px;
}

.delete-button.cancel {
  background-color: white;
  width: 88px;
  color: #2D2D2D;

}

.delete-buttons-wrapper {
  margin-top: 20px;
  justify-content: space-evenly;
  display: flex;
}

.item-to-delete-count-input {
  width: 210px;
  height: 40px;
  margin-top: 10px;
  top: 20px;
  left: 21px;
  color: white;
  text-align: center;
  border: solid 1px #4D4D4D;
  background-color: #262626;
}

.delete-window {
  border-top: solid 1px #4D4D4D;
  position: absolute;
  height: 133px;
  width: 250px;
  bottom: 0;
}

.delete-window-button {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #FA7272;
  width: 220px;
  height: 39px;
  border-radius: 8px;
  cursor: pointer;
  bottom: 20px;
}

.delete-window-button-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  bottom: 0;
  border-top: #4D4D4D 1px solid;
  width: 225px;
  height: 100px;
}

.item-description {
  width: 220px;
  max-height: 360px;
}

.item-name {
  font-size: 25px;
}

.close-cross {
  position: absolute;
  background-image: url("/public/UI/cross.png");
  background-size: 24px;
  height: 24px;
  width: 24px;
  cursor: pointer;
  top: 10px;
}

.close-button {
  display: flex;
  width: 220px;
  font-size: 25px;
  justify-content: flex-end
}

.item-image {
  background-repeat: no-repeat;
  background-size: 130px;
  height: 130px;
  width: 130px;
}

.item-image-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  border-bottom: #4D4D4D solid 1px;
  height: 200px;
  width: 220px;
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
