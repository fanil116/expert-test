<template>
    <div class="flex">
            <img :src="photo" alt="Photo" class="mr-2 w-40 h-40 object-cover">
            <div>
                <div class="flex items-center">
                    <p class="text-xl mr-1">{{ account.name }}</p>
                    <UButton icon="i-custom-shortcut" color="neutral" variant="ghost" size="xs"/>
                </div>
                <div class="flex">
                    <p class="text-gray-400">Кандидат на вакансию:</p>
                    <span class="text-blue-700 ml-2">Жадный благотваритель</span>
                    <UButton icon="i-custom-shortcut" color="neutral" variant="ghost" size="xs"/>
                    <p class="text-blue-700 ml-4">(14.08.2024 Отклик)</p>
                </div>
                <div v-if="account.status == 'viewed'" class="text-gray-400">Просмотрено</div>
                <div v-else class="text-gray-400">Не просмотрено</div>
                <div class="text-gray-400">Возраст
                    <span v-if="account.age">{{ account.age }}</span>
                    <span v-else>не указан</span>
                </div>
                <div class="text-amber-300 flex items-center">
                    <UIcon name="i-lucide-phone" class="size-7 mr-1" />
                    <a :href="`tel:+${account.phone}`" class="text-blue-700">+{{ account.phone }}</a>
                    <div v-for="(icon, index) in iconSocialName" :key="index">
                        <UButton :icon="icon" color="neutral" variant="ghost" size="xl" />
                    </div>
                </div>
                <div class="text-amber-300 flex items-center">
                    <UIcon name="i-lucide-mail" class="size-7 mr-1" />
                    <a :href="`mailto:${account.email}`" class="text-blue-500">{{ account.email }}</a>
                </div>
            </div>
        </div>
</template>
<script setup lang="ts">
    import type { AccountType } from "@/types/account"
    defineProps<{
        account: AccountType
        photo: string
    }>();
    const iconSocialName = ["logos:whatsapp-icon", "logos:telegram", "simple-icons:viber"]
</script>