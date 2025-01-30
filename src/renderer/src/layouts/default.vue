<template>
  <v-app>
    <AppTopBar />
    <v-main class="no-scrollbar">
      <router-view />
    </v-main>
    <div class="scale-control">
      <v-select
        v-model="dpi"
        :items="dpiOptions"
        label="选择页面 DPI"
        class="scale-select"
      ></v-select>
      <div class="scale-label">调整页面 DPI</div>
    </div>
  </v-app>
</template>

<script lang="ts" setup>
import { ref, watch } from 'vue';

const dpiOptions = ['75%', '100%', '125%', '150%', '175%', '200%']; // DPI 选项

const dpi = ref('100%'); // 默认值为100%

watch(dpi, (newDpi) => {
  document.documentElement.style.zoom = newDpi; // 动态调整根元素的缩放比例
});
</script>

<style scoped>
.no-scrollbar {
  overflow: hidden;
}

.scale-control {
  position: fixed;
  bottom: 10px;
  left: 50%;
  transform: translateX(-50%);
  width: 300px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.scale-select {
  margin-right: 10px;
}

.scale-label {
  margin-left: 10px;
}
</style>
