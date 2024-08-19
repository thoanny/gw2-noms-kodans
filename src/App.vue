<script setup>
import { ref } from 'vue';
import DataDebug from '@/components/DataDebug.vue';
import AppHeader from '@/components/AppHeader.vue';
import AppFooter from '@/components/AppFooter.vue';
import IconReload from '@/components/IconReload.vue';

import data from '@/data.json';

const DEBUG = false; // Check firstnames and lastnames' lists

const genders = ['féminin', 'masculin']; // Female, Male words in select list
const gender = ref(2); // Default gender: random
const fullname = ref('ʕ ꈍܫꈍʔ'); // Ref from API maintenance: "The API is beary tired ʕ ꈍܫꈍʔ. Scheduled reactivation: 23 August."

const setFullname = () => {
    fullname.value = null;

    // Words' genders:
    // 0 - Female
    // 1 - Male
    // 2 - Neutral
    const g = gender.value < 2 ? gender.value : Math.floor(Math.random() * 2);
    const firstnames = data.firstnames[g].concat(data.firstnames[2]);
    const lastnames = data.lastnames[g].concat(data.lastnames[2]);

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
    <DataDebug :data="data" v-if="DEBUG" />
    <div class="w-full min-h-[100dvh] flex items-center justify-center text-center bg-image">
        <div
            class="flex flex-col items-center justify-center gap-6 max-w-sm mx-auto z-20 py-6 text-white"
        >
            <AppHeader />
            <h2 class="text-xl font-semibold">
                Quel est ton nom kodan
                <select name="gender" id="gender" v-model="gender" @change="setFullname">
                    <option value="2">(aléatoire)</option>
                    <option v-for="(gender, g) in genders" :key="gender" :value="g">
                        {{ gender }}
                    </option></select
                >*&nbsp;?
            </h2>
            <div class="italic text-xs -mt-4 text-gray-400">
                *&nbsp;Ne correspond pas à votre identité de genre, ni celle de votre personnage,
                mais au genre de nom et de son adjectif accordé que vous souhaitez.
            </div>
            <h3 class="text-3xl font-bold text-white">
                {{ fullname }}
            </h3>
            <button v-if="gender !== ''" @click="setFullname">
                <IconReload />
            </button>
            <AppFooter />
        </div>
    </div>
</template>
