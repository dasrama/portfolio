<script setup>
const props = defineProps({
  type: { type: String, default: 'button' },
  loading: { type: Boolean, default: false },
  loadingText: { type: String, default: 'Loading...' },
  disabled: { type: Boolean, default: false },
  fullWidth: { type: Boolean, default: false },
})
</script>

<template>
  <button
    :type="props.type"
    :disabled="props.loading || props.disabled"
    :class="[
      'inline-flex items-center justify-center gap-2 rounded-lg bg-primary px-5 py-2.5 text-sm font-bold text-black shadow-[0_0_15px_rgba(57,255,20,0.25)] transition-all hover:bg-primary/90 disabled:cursor-not-allowed disabled:opacity-60',
      props.fullWidth ? 'w-full' : '',
    ]"
  >
    <svg
      v-if="props.loading"
      class="size-4 animate-spin"
      viewBox="0 0 24 24"
      fill="none"
      xmlns="http://www.w3.org/2000/svg"
      aria-hidden="true"
    >
      <circle cx="12" cy="12" r="10" stroke="currentColor" stroke-opacity="0.25" stroke-width="4" />
      <path d="M22 12a10 10 0 0 1-10 10" stroke="currentColor" stroke-width="4" />
    </svg>
    <span v-if="props.loading">{{ props.loadingText }}</span>
    <slot v-else />
  </button>
</template>
