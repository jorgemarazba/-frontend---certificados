<script setup lang="ts">
import Navbar from './components/Navbar.vue'
import FileTransferBanner from './components/FileTransferBanner.vue'
import DocumentosPanel from './components/Documentospenel.vue'  
</script>

<template>
  <Navbar />
  <FileTransferBanner />
  <DocumentosPanel />
</template>

<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
}

/* Evita desbordamiento en movil */
html, body {
  overflow-x: hidden;
  background-color: #f9fafb;
}
</style>
