<template>
  <transition name="modal">
    <div class="modal" @click="$emit('close')">
      <div class="modal-wrapper" @click.stop="">
        <div class="modal-header">
          <h2>{{ title }}</h2>
          <button @click="$emit('close')">&#x2715;</button>
        </div>
        <div class="modal-content">
          <slot></slot>
        </div>
      </div>
    </div>
  </transition>
</template>

<script setup>
const props = defineProps({
  title: {
    type: String,
    required: true,
  },
});

</script>

<style scoped>
/* animation */
.modal-enter .modal-leave-active {
  opacity: 0;
}
.modal-enter .modal-wrapper,
.modal-leave-active .modal-wrapper {
  transform: scale(1.2);
}
.modal {
  position: fixed;
  left: 0;
  top: 0;
  z-index: 99999999;
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: rgba(0, 0, 0, 0.6);
}
button {
  border: none;
  outline: none;
  border-radius: 10px;
  padding: 10px;
  background: rgb(76, 76, 250);
  cursor: pointer;
}
.modal-wrapper {
  width: 470px;
  height: 150px;
  margin: 10px;
  background: #ffffff;
  box-shadow: 0px 4px 77px rgba(0, 0, 0, 0.25);
  border-radius: 16px;
  display: flex;
  position: relative;
  padding: 20px;
  flex-direction: column;
  transition: all 0.3s;
}
.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>
