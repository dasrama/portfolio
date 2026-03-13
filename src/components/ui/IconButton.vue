<script setup>
const props = defineProps({
  icon: { type: String, required: true },
  label: { type: String, required: true },
  type: { type: String, default: 'button' },
  size: { type: String, default: 'md' },
})

const sizeClass = {
  sm: 'size-8',
  md: 'size-10',
  lg: 'size-12',
}
</script>

<template>
  <button
    :type="props.type"
    :aria-label="props.label"
    :title="props.label"
    :class="[
      'inline-flex items-center justify-center rounded-full border border-secondary/30 bg-white/5 text-secondary transition-all hover:scale-105 hover:border-secondary/60 hover:bg-secondary/10',
      sizeClass[props.size] ?? sizeClass.md,
    ]"
  >
    <span class="material-symbols-outlined">{{ props.icon }}</span>
  </button>
</template>
