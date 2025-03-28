<template>
  <div class="app">
    <button @click="openModal">Открыть модальное окно</button> <!-- Кнопка для открытия модалки -->
    <Modal
      :isOpen="isModalOpen"
      :onClose="closeModal"
    >
      <div class="rejection-form">
        <p class="rejection-reason">РАССКАЖИТЕ, ПОЧЕМУ ОТКАЗАЛИСЬ ОТ ВЫПОЛНЕНИЯ ЗАКАЗА?</p>
      </div>
    </Modal>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Modal from './components/Modal/modal.vue';

const isModalOpen = ref(false); // Флаг для отображения/скрытия модалки
const selectedOptions = ref([]);

const openModal = () => { // Открытие модалки
  isModalOpen.value = true;
};

const closeModal = () => { // Закрытие модалки
  isModalOpen.value = false;
};

</script>

<style>
.app {
  padding: 20px; /* Отступы внутри блока */
}
</style>