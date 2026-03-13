<script setup>
const props = defineProps({
  type: { type: String, default: 'button' },
  disabled: { type: Boolean, default: false },
  fullWidth: { type: Boolean, default: false },
})
</script>

<template>
  <button
    :type="props.type"
    :disabled="props.disabled"
    :class="[
      'rounded-lg bg-primary px-5 py-2.5 text-sm font-bold text-black shadow-[0_0_15px_rgba(57,255,20,0.25)] transition-all hover:scale-[1.02] hover:bg-primary/90 disabled:cursor-not-allowed disabled:opacity-50',
      props.fullWidth ? 'w-full' : '',
    ]"
  >
    <slot />
  </button>
</template>
