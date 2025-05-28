<template>
    <div class="mt-2 mb-4">
            <p class="mb-2 font-medium text-gray-400">Дела:</p>
            <UButton v-for="(item, index) in works" :key="index"    color="success" :variant="item.done ? 'subtle' : 'outline'" size="xl" class="mr-2 text-blue-50 w-35 cursor-pointer" :disabled="item.disabled">
                    {{ item.done ? item.labelDone : item.label }}
            </UButton>
    </div>
</template>
<script setup lang="ts">
    const works = [
        {
            label: 'Запланировать собеседование',
            labelDone: 'Собеседование запланировано',
            done: true,
            disabled: false,
        },
        {
            label: 'Создать видеозвонок',
            labelDone: 'Видеозвонок заплонирован',
            done: false,
            disabled: false,
        },
        {
            label: 'Запланировать событие',
            labelDone: 'Событие запланировано',
            done: false,
            disabled: true,
        },
        {
            label: 'Отправить запрос',
            labelDone: 'Запрос отправлен',
            done: false,
            disabled: false,
        },
    ]
</script>