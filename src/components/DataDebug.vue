<script setup>
defineProps(['data']);
</script>
<template>
    <div class="grid grid-cols-6 gap-6 p-6 text-white z-30 relative">
        <div v-for="list in data.firstnames" class="border p-6">
            <div v-for="name in list.sort((a, b) => a.localeCompare(b))">
                {{ name }}
            </div>
        </div>
        <div v-for="list in data.lastnames" class="border p-6">
            <div v-for="name in list.sort((a, b) => a.localeCompare(b))">
                {{ name }}
            </div>
        </div>
    </div>
</template>
