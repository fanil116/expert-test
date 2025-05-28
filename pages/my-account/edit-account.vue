<template>
    <div class="flex">
        <div v-for="(icon, index) in iconName" :key="index">
            <UButton :icon="`i-custom-${icon}`" color="neutral" variant="solid" size="xl" class="mr-2"/>
        </div>
    </div>
    <div v-if="account" class="mt-4">
        <AccountInfo :account="account" :photo="photo"/>
        <AccountWork />
        <div>
            <p class="font-medium mb-2 text-gray-400">Статус рассмотрения:</p>
            <StatusSteps :status="account.status"/>
            
        </div>
        <div class="mt-4 font-medium">
            <p class="text-3xl">Pikabu отлик</p>
            <p class="text-gray-400">Отлик с портала pikabu.</p>
        </div>
        <div class="mt-4 text-gray-400 font-medium">
            <p>Дата рождения: <span class="font-normal">{{ account.birth_date }}</span></p>
            <p>Граждантсво: <span class="font-normal">{{ getNationality }}</span></p>
        </div>
        <div class="mt-4">
            <p class="text-gray-400">Сопроводительное письмо</p>
        </div>
        <div class="bg-teal-400 flex p-6 mt-4 gap-2">
            <div class=" flex-1"><UIcon name="i-lucide-info" class="text-6xl" /></div>
            <div>
                <p class="font-medium">Файлы портфолио:</p>
                <AccountDescription :description="account.description"/>
            </div>
        </div>
    </div>
    <div v-else>{{ error }}</div>
</template>
<script setup lang="ts">
    import StatusSteps from '@/components/account/StatusSteps.vue';
    import AccountInfo from '@/components/account/AccountInfo.vue';
    import AccountDescription from '@/components/account/AccountDescription.vue';
    import AccountWork from '@/components/account/AccountWork.vue';
    import type { AccountType } from "@/types/account"
    let account = ref<AccountType | null>(null);
    let error = ref<string | null>(null);
    let photo = ref<string>("");
    const iconName = ["print", "pdf-files", "doc-file", "resume", "red-trash", "document-send", "like"];
    const baseUrl = "https://dev.jobcart.ru"

    onMounted(async () => {
        try {
            const response = await fetch(`${baseUrl}/wp-json/test/v2/app`);
            if (!response.ok) {
                throw new Error('Failed to fetch resume data');
            }
            const data = await response.json();
            account.value = data || [];
            photo.value = `${baseUrl}${account.value.photo}`
        } catch (err) {
            console.error('Error fetching resume:', err);
            error.value = 'Failed to load resume';
        }
    });
    const getNationality = computed((): string => {
        const nationality = account.value.description?.split('\r\n').find((el) => el.includes('Гражданство'))
        return nationality.split(':')[1]?.trim() ?? ''
    })
</script>
