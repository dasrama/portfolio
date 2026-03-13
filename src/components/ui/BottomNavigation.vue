<script setup>
const props = defineProps({
  items: {
    type: Array,
    default: () => [],
  },
  modelValue: {
    type: [String, Number],
    default: null,
  },
})

const emit = defineEmits(['update:modelValue', 'navigate'])

function onSelect(item, index) {
  const value = item.value ?? item.key ?? item.label ?? index
  emit('update:modelValue', value)
  emit('navigate', item)
}
</script>

<template>
  <nav class="fixed inset-x-0 bottom-0 z-50 border-t border-slate-700/40 bg-background-dark/95 backdrop-blur-md md:hidden">
    <ul class="grid" :style="{ gridTemplateColumns: `repeat(${Math.max(props.items.length, 1)}, minmax(0, 1fr))` }">
      <li v-for="(item, index) in props.items" :key="item.key ?? item.label ?? index">
        <button
          type="button"
          class="relative flex w-full flex-col items-center justify-center gap-1 py-2 text-xs transition-colors"
          :class="(props.modelValue === (item.value ?? item.key ?? item.label ?? index)) ? 'text-primary' : 'text-slate-400 hover:text-slate-100'"
          @click="onSelect(item, index)"
        >
          <span v-if="item.icon" class="material-symbols-outlined text-xl">{{ item.icon }}</span>
          <span>{{ item.label }}</span>
          <span v-if="item.badge" class="absolute right-4 top-1 rounded-full bg-primary px-1.5 text-[10px] font-bold text-black">{{ item.badge }}</span>
        </button>
      </li>
    </ul>
  </nav>
</template>
