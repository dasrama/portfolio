<script setup>
const props = defineProps({
  gap: { type: String, default: '0.75rem' },
  wrap: { type: Boolean, default: true },
  align: { type: String, default: 'center' },
  justify: { type: String, default: 'start' },
})
</script>

<template>
  <div
    class="flex"
    :class="props.wrap ? 'flex-wrap' : 'flex-nowrap'"
    :style="{ gap: props.gap, alignItems: props.align, justifyContent: props.justify }"
  >
    <slot />
  </div>
</template>
