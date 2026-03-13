<script setup>
const props = defineProps({
  icon: { type: String, default: 'add' },
  label: { type: String, default: 'Action' },
  bottom: { type: String, default: '1.5rem' },
  right: { type: String, default: '1.5rem' },
})
</script>

<template>
  <button
    type="button"
    :aria-label="props.label"
    :title="props.label"
    class="fixed z-40 inline-flex size-14 items-center justify-center rounded-full bg-primary text-black shadow-[0_10px_25px_rgba(57,255,20,0.35)] transition-all hover:scale-105 hover:bg-primary/90"
    :style="{ bottom: props.bottom, right: props.right }"
  >
    <span class="material-symbols-outlined">{{ props.icon }}</span>
  </button>
</template>
