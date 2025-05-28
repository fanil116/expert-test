<template>
    <div class="text-blue-700 font-medium flex">
        Резюме:
        <div v-if="description" class="whitespace-pre-wrap wrap-break-word ml-2" v-html="description" />
        <div v-else>Нет данных</div>
    </div>
</template>
<script setup lang="ts">
    defineProps<{
        description: string
    }>();
</script>