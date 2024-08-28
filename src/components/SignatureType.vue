<template>
  <div class="signature_type">
    <p class="signature_type--text">Type your signature here</p>
    <div class="signature_type--container">
      <input
        class="signature_type--container--input"
        type="text"
        placeholder="Type here"
        v-model="typedSignature"
      />
      <div class="signature_type--container--font-options">
        <label
          class="signature_type--container--font-options--label"
          v-for="(font, index) in fonts"
          :key="index"
          :class="{
            'signature_type--container--font-options--label--active':
              font === selectedFont,
          }"
        >
          <input
            class="signature_type--container--font-options--label--input"
            type="radio"
            :value="font"
            v-model="selectedFont"
          />
          <span
            class="signature_type--container--font-options--label--text"
            :style="{ fontFamily: font }"
          >
            {{ typedSignature || "Sample" }}
          </span>
        </label>
      </div>
    </div>

    <p class="signature_type--disclaimer">
      By continuing, I understand that this is a legal representation of my
      signature.
    </p>
  </div>
</template>

<script setup>
import { ref } from "vue";

const typedSignature = ref("");
const selectedFont = ref("sans-serif");

const fonts = ["sans-serif", "monospace", "fantasy", "cursive"];
</script>

<style scoped lang="scss">
.signature_type {
  &--text {
    font-size: .9rem;
    font-weight: 500;
  }
  &--container {
    &--input {
      width: 50%;
      padding: 8px;
      margin-top: 10px;
      border-radius: 5px;
      border: 1px solid #ccc;
      @media screen and (max-width: 768px) {
        width: 100%;
      }
    }
    &--input:focus {
      outline: none;
    }
    &--font-options {
      margin-top: 15px;
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 1rem;
      @media screen and (max-width: 768px) {
        grid-template-columns: 1fr;
      }
      &--label {
        margin-bottom: 10px;
        padding: 10px;
        text-align: center;
        border-radius: 8px;
        border: 1px solid #f1f1f1;
        display: flex;
        & input[type="radio"] {
          flex: 0 0 8%;
          max-width: 15px;
        }
        &--text {
          font-size: 1.5rem;
          flex: 0 0 92%;
        }
        &--active {
          background: #f5f8ff;
        }
      }
    }
  }
  &--disclaimer {
    margin-top: 10px;
    font-size: 0.9rem;
    color: #666;
  }
}
</style>
