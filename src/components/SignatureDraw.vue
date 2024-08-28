<template>
  <div class="signature_draw">
    <div class="signature_draw--container">
      <p class="signature_draw--container--text">
        Draw your signature directly below
      </p>
      <canvas
        class="signature_draw--container--canvas"
        ref="signatureCanvas"
        @mousedown="startDrawing"
        @mousemove="draw"
        @mouseup="stopDrawing"
        @mouseleave="stopDrawing"
      ></canvas>
      <button class="signature_draw--container--clear" @click="clearCanvas">
        <span>X</span>
        <span>Redo</span>
      </button>
    </div>

    <p class="signature_draw--disclaimer">
      By continuing, I understand that this is a legal representation of my
      signature.
    </p>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const isDrawing = ref(false);
const context = ref(null);
const signatureCanvas = ref(null);

const startDrawing = (event) => {
  isDrawing.value = true;
  context.value.beginPath();
  context.value.moveTo(event.offsetX, event.offsetY);
};

const draw = (event) => {
  if (!isDrawing.value) return;
  context.value.lineTo(event.offsetX, event.offsetY);
  context.value.stroke();
};

const stopDrawing = () => {
  isDrawing.value = false;
  context.value.closePath();
};

const clearCanvas = () => {
  context.value.clearRect(
    0,
    0,
    signatureCanvas.value.width,
    signatureCanvas.value.height
  );
};

onMounted(() => {
  signatureCanvas.value.width = signatureCanvas.value.offsetWidth;
  signatureCanvas.value.height = signatureCanvas.value.offsetHeight;
  context.value = signatureCanvas.value.getContext("2d");
  context.value.strokeStyle = "#000000"; // Set the stroke color
  context.value.lineWidth = 2; // Set the line width
});
</script>

<style scoped lang="scss">
.signature_draw {
  &--container {
    text-align: center;
    &--text {
      font-size: 0.9rem;
      color: #0f0f0f;
      text-align: start;
      padding: 10px 0;
    }
    &--canvas {
      width: 100%;
      height: 150px;
      border: 1px dashed #ccc;
      border-radius: 5px;
      cursor: crosshair;
    }

    &--clear {
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
        transition-duration: 0.3s;
        span {
          color: white;
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
