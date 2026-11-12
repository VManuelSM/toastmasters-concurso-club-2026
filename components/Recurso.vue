<script setup lang="ts">
// Imagen servida desde public/, con la ruta base del sitio (GitHub Pages publica en una subcarpeta).
defineProps<{ src: string, alt?: string }>()
const base = import.meta.env.BASE_URL
</script>

<template>
  <img :src="base + src" :alt="alt">
</template>
