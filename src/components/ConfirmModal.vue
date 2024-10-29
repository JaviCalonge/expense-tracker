<template>
  <div v-if="show" class="confirm-overlay">
    <div class="confirm-box">
      <p>{{ message }}</p>
      <button @click="confirm">Sí</button>
      <button @click="cancel">No</button>
    </div>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from "vue";

const props = defineProps({
  show: Boolean,
  message: {
    type: String,
    default: "¿Estás seguro de que deseas continuar?",
  },
});

const emit = defineEmits(["confirm", "cancel"]);

const confirm = () => {
  emit("confirm");
};

const cancel = () => {
  emit("cancel");
};

</script>

<style scoped>
.confirm-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}
.confirm-box {
  background-color: #fff;
  border-radius: 8px;
  padding: 20px;
  text-align: center;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}
.confirm-box p {
  margin: 0 0 15px;
  font-size: 16px;
  color: #333;
}
.confirm-box button {
  padding: 10px 20px;
  margin: 0 5px;
  font-size: 14px;
  border: none;
  cursor: pointer;
}
button:first-of-type {
  background-color: #4caf50;
  color: white;
}
button:last-of-type {
  background-color: #f44336;
  color: white;
}
</style>
