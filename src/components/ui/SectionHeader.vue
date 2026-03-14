<script setup>
const props = defineProps({
  icon: { type: String, default: '' },
  eyebrow: { type: String, default: '' },
  title: { type: String, required: true },
  subtitle: { type: String, default: '' },
})
</script>

<template>
  <div class="mb-8">
    <div class="flex items-center gap-4">
      <span v-if="props.icon" class="material-symbols-outlined text-3xl text-primary">{{ props.icon }}</span>
      <div>
        <p v-if="props.eyebrow" class="text-xs font-bold uppercase tracking-[0.2em] text-secondary">{{ props.eyebrow }}</p>
        <h2 class="text-3xl font-bold">{{ props.title }}</h2>
      </div>
    </div>

    <p v-if="props.subtitle" class="mt-2 max-w-2xl text-slate-400">{{ props.subtitle }}</p>

    <div v-if="$slots.action" class="mt-4">
      <slot name="action" />
    </div>
  </div>
</template>
