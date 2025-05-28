<template>
    <div class="flex items-center gap-2 gap-x-6 flex-wrap text-white max-w-[1000px]">
      <div
        v-for="(step, index) in steps"
        :key="step.key"
        class="px-3 h-11 relative flex items-center"
        :class="[
          isActive(index) ? 'bg-gray-600 text-white' : 'bg-gray-300 text-gray-800',
          'w-[140px] arrow'
        ]"
      >
        <span class="text-sm leading-[1]">{{ step.label }}</span>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  const props = defineProps({
    status: String
  })
  
  // Шаги в нужном порядке
  const steps = [
    { key: 'new', label: 'Новое' },
    { key: 'viewed', label: 'Просмотрено' },
    { key: 'invited', label: 'Отправлено приглашение' },
    { key: 'interview', label: 'Назначено собеседование'},
    { key: 'no-show', label: 'Не дошел'},
    { key: 'done', label: 'Проведено собеседование' },
    { key: 'waiting', label: 'Ожидание ответа соискателя' },
    { key: 'decision', label: 'Принятие решения' },
    { key: 'accepted', label: 'Принят' },
    { key: 'rejected', label: 'Отклонено/Отказ' },
    { key: 'archived', label: 'Архивировано' },
  ]
  
  const activeIndex = computed((): number => steps.findIndex(item => item.key === props.status))
  
  const isActive = (index: number) => {
    return index <= activeIndex.value
  }
  </script>
  
  <style scoped>
  .arrow::after {
    content: '';
    position: absolute;
    right: -19px;
    top: 50%;
    transform: translateY(-50%);
    width: 20px;
    height: 45px;
    background-color: inherit;
    z-index: 1;
    clip-path: polygon(100% 50%, 0 0, 0 100%);
  }
  </style>
  