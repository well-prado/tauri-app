<script setup lang="ts">
// import { emit } from '@tauri-apps/api/event';
import { ref } from 'vue';
import { useDropzone } from 'vue3-dropzone';

const uploadQueue = ref<File[]>([]);

const { getRootProps, getInputProps, isDragActive } = useDropzone({
  onDrop: () => {},
  multiple: true,
  noClick: true,
  noKeyboard: true,
});

// function emitUploadProgress(progress: number) {
//   emit('progress', {
//     progress,
//   });
// }

// function handleStrartUpload(files: File[]) {
//   uploadQueue.value = files;

//   setTimeout(() => {
//     emitUploadProgress(10);
//   }, 500 * 1);
//   setTimeout(() => {
//     emitUploadProgress(20);
//   }, 500 * 2);
//   setTimeout(() => {
//     emitUploadProgress(30);
//   }, 500 * 3);
//   setTimeout(() => {
//     emitUploadProgress(40);
//   }, 500 * 4);
//   setTimeout(() => {
//     emitUploadProgress(50);
//   }, 500 * 5);
//   setTimeout(() => {
//     emitUploadProgress(60);
//   }, 500 * 6);
//   setTimeout(() => {
//     emitUploadProgress(70);
//   }, 500 * 7);
//   setTimeout(() => {
//     emitUploadProgress(80);
//   }, 500 * 8);
//   setTimeout(() => {
//     emitUploadProgress(90);
//   }, 500 * 9);
//   setTimeout(() => {
//     emitUploadProgress(100);
//   }, 500 * 10);
// }

// function handleCancelUpload() {
//   uploadQueue.value = [];
// }

// function handleQuitApp() {
//   emit('quit');
// }

const status =
  uploadQueue.value.length > 0 ? 'accept' : isDragActive ? 'active' : 'pending';
</script>

<template>
  <div class="space-y-1">
    <div
      v-bind="getRootProps()"
      class="text-white/80 m-4 px-4 h-24 flex items-center border border-dashed rounded justify-center"
    >
      <input v-bind="getInputProps()" />

      <div v-if="status === 'active'">
        <p>Start upload</p>
      </div>

      <div v-else-if="status === 'accept'">
        <p>Uploading {{ uploadQueue.length }} file(s)</p>
      </div>
    </div>
  </div>
</template>
