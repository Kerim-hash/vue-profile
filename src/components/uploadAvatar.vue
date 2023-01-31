<template>
  <div class="upload">
    <div
      class="upload-preview"
      :style="{ 'background-image': `url(${imageData})` }"
      @click="chooseImage"
    >
      <img
        v-if="!imageData"
        class="upload-avatar"
        src="https://api.netex.land/uploads/users/86257789.jpeg"
        alt="avatar"
      />
      <input
        class="file-input"
        ref="fileInput"
        type="file"
        accept="image/gif, image/jpeg, image/png"
        @input="onSelectFile"
      />
    </div>

    <div class="upload-inner">
      <button class="upload-download" @click="chooseImage">
        <img class="upload-icon" :src="DownloadIcon" alt="download-icon" />
      </button>
      <button class="upload-download" @click="modalValue = true">
        <img class="upload-icon" :src="DeleteIcon" alt="download-icon" />
      </button>
    </div>

    <modal
      title="Вы уверены, что хотите удалить фотографию?"
      v-show="modalValue"
      @close="modalValue = !modalValue"
    >
      <div>
        <div class="upload-items">
          <button
            class="upload-button--cancel"
            @click="modalValue = !modalValue"
          >
            отменить
          </button>
          <button
            class="upload-button--success"
            @click="(imageData = null), (modalValue = !modalValue)"
          >
            да, удалить
          </button>
        </div>
      </div>
    </modal>
  </div>
</template>

<script setup>
import { ref } from "vue";
import DownloadIcon from "../assets/downloading.png";
import DeleteIcon from "../assets/delete.png";
import Modal from "./modal.vue";

// state
const fileInput = ref(null);
const imageData = ref(null);
const modalValue = ref(false);

const chooseImage = () => {
  fileInput.value.click();
};

const emit = defineEmits(["update:modelValue"]);

const onSelectFile = () => {
  const input = fileInput.value;
  const files = input.files;
  if (files && files[0]) {
    const reader = new FileReader();
    reader.onload = (e) => {
      imageData.value = e.target.result;
    };
    reader.readAsDataURL(files[0]);
    emit("update:modelValue", files[0]);
  }
};
</script>

<style lang="scss">
.upload {
  display: flex;
  &-avatar,
  &-preview {
    display: block;
    width: 200px;
    height: 200px;
    cursor: pointer;
    background-size: cover;
    background-position: center center;
    object-fit: cover;
    background: "https://api.netex.land/uploads/users/86257789.jpeg";
    border-radius: 12px;
  }
  &-inner {
    margin-left: 20px;
  }
  &-download {
    height: 40px;
    width: 40px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    background: linear-gradient(50deg, #ff3030 0%, #97baf6 97.19%);
    cursor: pointer;
    &:first-child {
      margin-bottom: 10px;
    }
    &:hover {
      opacity: 0.7;
      background: linear-gradient(120deg, #ff3030 0%, #97baf6 97.19%);
    }
  }
  &-icon {
    max-width: 100%;
  }
  &-items {
    display: flex;
    margin-top: 20px;
  }
  &-button {
    &--success,
    &--cancel {
      padding: 16px 32px;
      border: none;
      display: block;
      border-radius: 12px;
      color: #fff;
    }
    &--cancel {
      background: linear-gradient(120deg, #ff3030 0%, #97baf6 97.19%);
      margin-right: 10px;
    }
    &--success {
      background: linear-gradient(120deg, #00ff55 0%, #97baf6 97.19%);
    }
  }
}

.avatar:hover {
  background: #e0e0e0;
}
.file-input {
  display: none;
}
</style>
