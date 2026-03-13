<script setup>
import { computed } from 'vue'

const props = defineProps({
  tabs: {
    type: Array,
    default: () => [],
  },
  modelValue: {
    type: [String, Number],
    default: null,
  },
})

const emit = defineEmits(['update:modelValue', 'change'])

const active = computed(() => {
  if (props.modelValue !== null) return props.modelValue
  return props.tabs[0]?.value ?? props.tabs[0]?.key ?? 0
})

function pick(tab, index) {
  const value = tab.value ?? tab.key ?? index
  emit('update:modelValue', value)
  emit('change', tab)
}
</script>

<template>
  <div>
    <div class="inline-flex rounded-xl border border-secondary/20 bg-white/5 p-1">
      <button
        v-for="(tab, index) in props.tabs"
        :key="tab.key ?? tab.label ?? index"
        type="button"
        class="rounded-lg px-4 py-2 text-sm font-medium transition-colors"
        :class="(active === (tab.value ?? tab.key ?? index)) ? 'bg-primary text-black' : 'text-slate-300 hover:text-white'"
        @click="pick(tab, index)"
      >
        {{ tab.label }}
      </button>
    </div>

    <div class="mt-4">
      <slot name="panel" :active="active" />
    </div>
  </div>
</template>
