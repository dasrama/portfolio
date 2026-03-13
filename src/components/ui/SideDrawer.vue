<script setup>
const props = defineProps({
  modelValue: { type: Boolean, default: false },
  title: { type: String, default: 'Menu' },
  side: { type: String, default: 'left' },
})

const emit = defineEmits(['update:modelValue', 'close'])

function close() {
  emit('update:modelValue', false)
  emit('close')
}
</script>

<template>
  <Teleport to="body">
    <transition name="fade">
      <div v-if="props.modelValue" class="fixed inset-0 z-[90] bg-black/50" @click="close"></div>
    </transition>

    <transition :name="props.side === 'right' ? 'slide-right' : 'slide-left'">
      <aside
        v-if="props.modelValue"
        class="fixed top-0 z-[100] h-screen w-80 max-w-[85vw] border-slate-700/40 bg-background-dark p-5 shadow-2xl"
        :class="props.side === 'right' ? 'right-0 border-l' : 'left-0 border-r'"
      >
        <div class="mb-6 flex items-center justify-between">
          <h3 class="text-lg font-bold text-white">{{ props.title }}</h3>
          <button type="button" class="rounded-md p-1 text-slate-400 hover:bg-white/5 hover:text-white" @click="close">
            <span class="material-symbols-outlined">close</span>
          </button>
        </div>
        <slot :close="close" />
      </aside>
    </transition>
  </Teleport>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.slide-left-enter-active,
.slide-left-leave-active,
.slide-right-enter-active,
.slide-right-leave-active {
  transition: transform 0.25s ease;
}
.slide-left-enter-from,
.slide-left-leave-to {
  transform: translateX(-100%);
}
.slide-right-enter-from,
.slide-right-leave-to {
  transform: translateX(100%);
}
</style>
