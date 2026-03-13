<script setup>
const props = defineProps({
  title: { type: String, default: 'Portfolio' },
  sticky: { type: Boolean, default: true },
})
</script>

<template>
  <header
    :class="[
      'z-50 w-full border-b border-slate-200/70 bg-background-dark/80 px-6 py-4 backdrop-blur-md dark:border-slate-800/50',
      props.sticky ? 'sticky top-0' : '',
    ]"
  >
    <div class="mx-auto flex w-full max-w-7xl items-center justify-between gap-4">
      <div class="flex items-center gap-3">
        <slot name="left">
          <div class="flex size-9 items-center justify-center rounded-lg bg-primary text-black">
            <span class="material-symbols-outlined text-lg">terminal</span>
          </div>
        </slot>
        <h2 class="text-lg font-bold tracking-tight text-white">{{ props.title }}</h2>
      </div>

      <div class="hidden items-center gap-6 md:flex">
        <slot name="center" />
      </div>

      <div class="flex items-center gap-3">
        <slot name="right" />
      </div>
    </div>
  </header>
</template>
