<template> 
  <div v-if="isOpen" class="modal-overlay" @click.self="handleClose">  <!-- Если модалка открыто, показываем -->
    <div class="modal">
      <button class="close-btn" @click="handleClose">×</button> <!-- Кнопка закрытия модалки -->
      <div>
        <h2 class="modal-title">
          ОТКАЗАТЬСЯ ОТ ВЫПОЛНЕНИЯ ЗАКАЗА <strong>№ У00017711</strong>
        </h2>
        <p class="modal-subtitle">
          РАССКАЖИТЕ, ПОЧЕМУ ОТКАЗАЛИСЬ<br />ОТ ВЫПОЛНЕНИЯ ЗАКАЗА?
        </p>
        <div class="rejection-options"> <!-- Список причин отказа -->
          <label
            v-for="option in options"
            :key="option.value"
            class="option-item"
          >
            <input
              type="checkbox"
              :value="option.value"
              v-model="selectedOptions"
            />
            <span class="checkmark"></span>
            <span class="option-text">{{ option.label }}</span>
          </label>
        </div>
        <button class="submit-btn" @click="submitRejection">ОТПРАВИТЬ</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, defineProps, defineEmits } from 'vue';

// Определяем входные параметры (пропсы)
const props = defineProps({
  isOpen: Boolean,
  onClose: Function,
});

const emits = defineEmits(['submit']);

const options = [ // Список причин отказа
  { value: 'date', label: 'Не подходит дата или время' },
  { value: 'weight', label: 'Не подходит тоннаж груза' },
  { value: 'volume', label: 'Не подходит объем груза' },
  { value: 'type', label: 'Не подходит тип фургона' },
  { value: 'pass', label: 'Нет пропуска в МКАД ТТК СК' },
  { value: 'breakdown', label: 'Поломка машины/авария' },
  { value: 'sick', label: 'Заболел' },
  { value: 'sanitization', label: 'Нет санобработки' },
  { value: 'medical', label: 'Нет мед. книжки' },
  { value: 'hydroboard', label: 'Нет гидроборта' },
  { value: 'tent', label: 'Нет растентовки' },
  { value: 'rate', label: 'Не устраивает ставка за рейс' },
  { value: 'route', label: 'Не устраивает маршрут' },
  { value: 'other', label: 'Другое' },
];

const selectedOptions = ref([]);

const handleClose = () => { // Функция закрытия модального окна
  props.onClose();
};

const submitRejection = () => { // Функция закрытия модального окна (при клике закрывается модалка)
  emits('submit', selectedOptions.value);
  handleClose();
};
</script>

<style scoped src="./Modal.css"></style>
