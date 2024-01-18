<script setup lang="ts">
import { WebviewWindow } from '@tauri-apps/api/window';
import { ref, watchEffect } from 'vue';

const webviewStore = ref<WebviewWindow | null>(null);

const createWindow = async () => {
  const webview = new WebviewWindow('second-screen', {
    url: '../nested/index.html',
  });

  webviewStore.value = webview;
};

async function goFullScreen() {
  if (webviewStore.value) {
    await webviewStore.value.setFullscreen(true);
  }
}

watchEffect(() => {
  if (webviewStore.value) {
    webviewStore.value.isFullscreen().then(isFullscreen => {
      if (!isFullscreen) {
        goFullScreen();
      }
    });
  }
});
</script>

<template>
  <div class="flex items-center justify-center h-screen">
    <button @click="createWindow">Open second window</button>
  </div>
</template>
