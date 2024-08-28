<template>
  <div class="signature">
    <div class="signature--header">
      <span class="signature--header--number">3</span>
      <span class="signature--header--text">E-signature</span>
    </div>

    <div class="signature--tab">
      <button
        :class="{ 'signature--tab--list': true, active: activeTab === 'type' }"
        @click="activeTab = 'type'"
      >
        Type
      </button>
      <button
        :class="{
          'signature--tab--list': true,
          active: activeTab === 'upload',
        }"
        @click="activeTab = 'upload'"
      >
        Upload
      </button>
      <button
        :class="{ 'signature--tab--list': true, active: activeTab === 'draw' }"
        @click="activeTab = 'draw'"
      >
        Draw
      </button>
    </div>

    <div class="signature--content">
      <SignatureType v-if="activeTab === 'type'" />
      <SignatureUpload v-if="activeTab === 'upload'" />
      <SignatureDraw v-if="activeTab === 'draw'" />
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import SignatureType from "./components/SignatureType.vue";
import SignatureUpload from "./components/SignatureUpload.vue";
import SignatureDraw from "./components/SignatureDraw.vue";
const activeTab = ref("type");
</script>

<style scoped lang="scss">
.signature {
  max-width: 600px;
  margin: auto;
  &--header {
    display: flex;
    gap: 4px;
    align-items:center;
    margin-bottom: 10px;
    &--number {
      font-size: 16px;
      font-weight: 500;
      border: 1px solid #f0f0f0;
      height: 32px;
      width: 32px;
      border-radius: 50%;
      display: flex;
      justify-content: center;
      align-items: center;
      color: #1f47f4;
      font-weight: 500;
    }
    &--text {
      font-size: 16px;
      font-weight: 500;
      color: #1f47f4;
      font-weight: 600;
    }
  }
  &--tab {
    display: flex;
    border-radius: 4px;
    overflow: hidden;
    &--list {
      padding: 10px;
      border: 1px solid #ccc;
      background-color: #f0f0f0;
      cursor: pointer;
      width: 100%;
    }
    .active {
      background-color: #1f47f4;
      color: white;
    }
  }
  &--content {
    max-width: 600px;
    margin: auto;
    font-family: Arial, sans-serif;
    border-left: 1px solid #ccc;
    border-right: 1px solid #ccc;
    border-bottom: 1px solid #ccc;
    padding: 16px;
    max-height: 500px;
    height: 100%;
    width: 100%;
    aspect-ratio: 1.8;
  }
}
</style>
