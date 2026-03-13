<script setup>
const props = defineProps({
  items: {
    type: Array,
    default: () => [],
  },
})

const emit = defineEmits(['navigate'])
</script>

<template>
  <nav aria-label="Breadcrumb" class="text-sm">
    <ol class="flex flex-wrap items-center gap-2 text-slate-400">
      <li v-for="(item, index) in props.items" :key="item.key ?? item.label ?? index" class="inline-flex items-center gap-2">
        <button
          type="button"
          class="transition-colors hover:text-secondary"
          :class="index === props.items.length - 1 ? 'cursor-default font-semibold text-slate-100 hover:text-slate-100' : ''"
          :disabled="index === props.items.length - 1"
          @click="emit('navigate', item, index)"
        >
          {{ item.label }}
        </button>
        <span v-if="index < props.items.length - 1" class="material-symbols-outlined text-base text-slate-600">chevron_right</span>
      </li>
    </ol>
  </nav>
</template>
