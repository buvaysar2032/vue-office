<script setup>
import {onMounted, ref} from 'vue';
import CoordinatesDisplay from "@/components/CoordinatesDisplay.vue";

const marker = ref(null);
const officeMap = ref(null);
const xCoord = ref(0);
const yCoord = ref(0);
const isDragging = ref(false);

onMounted(() => {
  officeMap.value.addEventListener('mousemove', (event) => {
    if (isDragging.value) {
      xCoord.value += event.movementX
      yCoord.value += event.movementY

      xCoord.value = Math.max(0, xCoord.value);
      xCoord.value = Math.min(xCoord.value, officeMap.value.offsetWidth - marker.value.offsetWidth);

      yCoord.value = Math.max(0, yCoord.value);
      yCoord.value = Math.min(yCoord.value, officeMap.value.offsetHeight - marker.value.offsetHeight);

      if (Math.abs(event.offsetX - xCoord.value) > marker.value.offsetWidth && event.offsetX > marker.value.offsetWidth) {
        xCoord.value = event.offsetX;
      }
      if (Math.abs(event.offsetY - yCoord.value) > marker.value.offsetHeight && event.offsetY > marker.value.offsetHeight) {
        yCoord.value = event.offsetY;
      }
    }
  });

  document.addEventListener('mouseup', () => {
    isDragging.value = false;
  });
});
</script>

<template>
  <div class="wrap">
    <div class="office-map" ref="officeMap">
      <span
          class="marker"
          ref="marker"
          @mousedown.prevent="isDragging = true"
          :style="{ left: xCoord + 'px', top: yCoord + 'px' }"
      >
      </span>
    </div>

    <CoordinatesDisplay :xCoord="xCoord" :yCoord="yCoord"/>
  </div>
</template>

<style scoped>
.wrap {
  display: flex;
  align-items: center;
  flex-direction: column;
  position: relative;
}

.office-map {
  position: relative;
  width: 1200px;
  height: 480px;
  background-image: url('/1.png');
  background-size: cover;
  background-position: center;
}

.marker {
  width: 20px;
  height: 20px;
  background-color: red;
  position: absolute;
  cursor: pointer;
  border-radius: 50%;
}
</style>