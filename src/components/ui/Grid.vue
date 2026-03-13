<script setup>
import { computed } from 'vue'

const props = defineProps({
  cols: { type: Number, default: 1 },
  gap: { type: String, default: '1rem' },
  minColWidth: { type: String, default: '' },
})

const gridStyle = computed(() => {
  if (props.minColWidth) {
    return {
      gap: props.gap,
      gridTemplateColumns: `repeat(auto-fit, minmax(${props.minColWidth}, 1fr))`,
    }
  }

  return {
    gap: props.gap,
    gridTemplateColumns: `repeat(${Math.max(1, props.cols)}, minmax(0, 1fr))`,
  }
})
</script>

<template>
  <div class="grid" :style="gridStyle">
    <slot />
  </div>
</template>
