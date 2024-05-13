<template>
  <v-container>
    <v-row>
      <v-col cols="6">
        <v-text-field v-model="sizeX" label="Size X"></v-text-field>
      </v-col>
      <v-col cols="6">
        <v-text-field v-model="sizeY" label="Size Y"></v-text-field>
      </v-col>
    </v-row>

    <v-row v-if="parseInt(sizeX) > 0 && parseInt(sizeY) > 0">
      <v-col v-for="col in parseInt(sizeX)" :key="col" cols="auto">
        <v-row>
          <v-col v-for="row in parseInt(sizeY)" :key="row" cols="auto">
            <div
              class="grid-item"
              :class="{ blue: isBlue[row - 1][col - 1] }"
              @mouseover="toggleColor(row - 1, col - 1)"
            ></div>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
import { ref, watch } from "vue";

const sizeX = ref("");
const sizeY = ref("");
const isBlue = ref([]);

const initializeGrid = () => {
  isBlue.value = Array.from({ length: parseInt(sizeY.value) }, () =>
    Array.from({ length: parseInt(sizeX.value) }, () => false)
  );
};

const toggleColor = (row, col) => {
  isBlue.value[row][col] = !isBlue.value[row][col];
};

watch([sizeX, sizeY], () => {
  initializeGrid();
});
</script>

<style scoped>
.grid-item {
  width: 36px;
  height: 36px;
  background-color: white;
  border: 1px solid #ccc;
}
.blue {
  background-color: blue !important;
}
</style>
