<script setup>
const props = defineProps({
  as: { type: String, default: 'article' },
  padded: { type: Boolean, default: true },
  interactive: { type: Boolean, default: false },
})
</script>

<template>
  <component
    :is="props.as"
    :class="[
      'rounded-2xl border border-secondary/20 bg-surface/70 backdrop-blur-sm',
      props.padded ? 'p-6' : '',
      props.interactive ? 'transition-all hover:-translate-y-0.5 hover:border-secondary/45' : '',
    ]"
  >
    <slot />
  </component>
</template>
