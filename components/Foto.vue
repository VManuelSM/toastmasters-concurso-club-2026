<script setup lang="ts">
import { computed, ref } from 'vue'

// Foto circular del socio desde public/fotos/<slug>.jpg. Si no existe, quedan las iniciales.
const props = defineProps<{ slug: string, nombre: string }>()
const base = import.meta.env.BASE_URL
const visible = ref(true)
const iniciales = computed(() => {
  const partes = props.nombre.replace(/\b[A-Z]\.\s*/g, '').trim().split(/\s+/)
  return (partes[0][0] + (partes[1]?.[0] ?? '')).toUpperCase()
})
</script>

<template>
  <span class="foto" :aria-label="nombre">
    <span class="foto__iniciales" aria-hidden="true">{{ iniciales }}</span>
    <img v-if="visible" :src="`${base}fotos/${slug}.jpg`" alt="" @error="visible = false">
  </span>
</template>

<style scoped>
.foto {
  align-items: center;
  background: var(--brand-primary);
  border-radius: 50%;
  color: var(--text-inverse, #fff);
  display: inline-flex;
  flex: none;
  height: 1.9rem;
  justify-content: center;
  overflow: hidden;
  position: relative;
  width: 1.9rem;
}

.foto__iniciales {
  font-family: var(--font-main);
  font-size: 0.62rem;
  font-weight: 600;
}

.foto img {
  height: 100%;
  inset: 0;
  object-fit: cover;
  position: absolute;
  width: 100%;
}
</style>
