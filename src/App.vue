<script setup>
import { ref, computed } from 'vue';

import data from '@/data.json';

const genders = ['féminin', 'masculin'];
const gender = ref('');
const fullname = ref(null);

const setFullname = () => {
    fullname.value = null;

    const firstnames =
        gender.value.length !== 0 ? data.firstname[gender.value].concat(data.firstname[2]) : null;

    const lastnames =
        gender.value.length !== 0 ? data.lastname[gender.value].concat(data.lastname[2]) : null;

    if (firstnames && lastnames) {
        const fid = Math.floor(Math.random() * firstnames.length);
        const lid = Math.floor(Math.random() * lastnames.length);
        const firstname = firstnames[fid];
        const lastname = lastnames[lid];
        fullname.value = `${firstname} ${lastname}`;
    }
};
</script>

<template>
    <div class="flex flex-col items-center justify-center text-center h-screen gap-6">
        <div class="text-xl font-semibold">
            Quel est ton nom kodan
            <select name="gender" id="gender" v-model="gender" class="border" @change="setFullname">
                <option value="">---</option>
                <option v-for="(gender, g) in genders" :key="gender" :value="g">
                    {{ gender }}
                </option>
            </select>
            ?
        </div>
        <div class="text-2xl font-bold">{{ fullname }}</div>
        <button v-if="gender !== ''" @click="setFullname" class="bg-gray-100 py-2 px-4">
            Générer
        </button>
    </div>
</template>

<style scoped>
h2 {
    @apply text-xl font-bold my-8;
}
</style>
