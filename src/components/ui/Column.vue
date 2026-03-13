<script setup>
const props = defineProps({
  gap: { type: String, default: '0.75rem' },
  align: { type: String, default: 'stretch' },
})
</script>

<template>
  <div class="flex flex-col" :style="{ gap: props.gap, alignItems: props.align }">
    <slot />
  </div>
</template>
