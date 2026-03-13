<script setup>
const props = defineProps({
  size: { type: String, default: 'xl' },
  as: { type: String, default: 'div' },
})

const sizes = {
  md: 'max-w-3xl',
  lg: 'max-w-5xl',
  xl: 'max-w-7xl',
  full: 'max-w-none',
}
</script>

<template>
  <component :is="props.as" :class="['mx-auto w-full px-6', sizes[props.size] ?? sizes.xl]">
    <slot />
  </component>
</template>
