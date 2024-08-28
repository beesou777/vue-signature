<template>
  <div class="signature_upload">
    <div class="signature_upload--container">
      <p class="signature_upload--container--text">Upload your signature</p>
      <div class="signature_upload--container--input_container">
        <input
          class="signature_upload--container--input_container--input"
          type="file"
          @change="onFileSelected"
          accept="image/*"
        />
        <p class="signature_upload--container--input_container--text">
          click to upload
        </p>
      </div>
      <div v-if="uploadedImage" class="signature_upload--container--preview">
        <img :src="uploadedImage" alt="Uploaded Signature" />
        <button
          class="signature_upload--container--preview--remove"
          @click="removeImage"
        >
          <span>X</span>
          <span>Remove</span>
        </button>
      </div>
    </div>

    <p class="signature_upload--disclaimer">
      By continuing, I understand that this is a legal representation of my
      signature.
    </p>
  </div>
</template>

<script setup>
import { ref } from "vue";

const uploadedImage = ref(null);

const onFileSelected = (event) => {
  const file = event.target.files[0];
  if (file) {
    const reader = new FileReader();
    reader.onload = (e) => {
      uploadedImage.value = e.target.result;
    };
    reader.readAsDataURL(file);
  }
};

const removeImage = () => {
  uploadedImage.value = null;
};
</script>

<style scoped lang="scss">
.signature_upload {
  &--container {
    text-align: center;
    &--text {
      font-size: 0.9rem;
      color: #0f0f0f;
      text-align: start;
      padding: 10px 0;
    }
    &--input_container {
      position: relative;
      height: 150px;
      background: #f7f7f7;
      border-radius: 8px;
      &--input {
        cursor: pointer;
        height: 150px;
        width: 100%;
        opacity: 0;
        position: relative;
        z-index: 10;
      }
      &--text {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        font-size: 1.2rem;
        color: #ccc;
      }
    }
    &--preview {
      margin-top: 15px;
      display: flex;
      flex-direction: column;
      & img {
        max-width: 100%;
        max-height: 150px;
        height: auto;
        aspect-ratio: 300/200;
        object-fit: cover;
        border-radius: 5px;
        border: 1px solid #ccc;
        object-position: center;
      }
      &--remove {
        align-items: center;
        margin-top: 10px;
        border: none;
        padding: 8px 12px;
        border-radius: 5px;
        cursor: pointer;
        background: transparent;
        display: flex;
        width: fit-content;
        margin: auto;
        margin-top: 5px;
        span:first-child {
          margin-right: 5px;
          background-color: #ff0000;
          color: #fff;
          padding: 2px;
          height: 15px;
          width: 15px;
          font-size: 10px;
          border-radius: 50%;
          display: inline-block;
        }
        span:last-child {
          color: #ff0000;
          font-weight: bold;
        }

        &:hover {
          background-color: #ff0000;
          transition-duration: .3s;
          span {
            color: white;
          }
        }
      }
    }
  }
  &--disclaimer {
    margin-top: 10px;
    font-size: 0.9rem;
    color: #0f0f0f;
    text-align: start;
  }
}
</style>
