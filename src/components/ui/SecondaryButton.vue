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
      'rounded-lg border border-secondary/40 bg-white/5 px-5 py-2.5 text-sm font-bold text-slate-100 backdrop-blur-sm transition-all hover:scale-[1.02] hover:border-secondary/70 hover:bg-secondary/10 disabled:cursor-not-allowed disabled:opacity-50',
      props.fullWidth ? 'w-full' : '',
    ]"
  >
    <slot />
  </button>
</template>
