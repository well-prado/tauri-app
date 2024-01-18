<script setup lang="ts">
import { WebviewWindow } from '@tauri-apps/api/window';

const createWindow = async () => {
  const newWindowMeta = { id: Date.now().toString(), title: 'Tauri Studio' };
  const webview = new WebviewWindow(newWindowMeta.id, {
    url: '',
  });

  await webview.emit('tauri://create-window', newWindowMeta);
};
</script>

<template>
  <div class="flex items-center justify-center h-screen">
    <button @click="createWindow">Open second window</button>
  </div>
</template>
