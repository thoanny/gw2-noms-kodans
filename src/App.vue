<script setup>
import { ref } from 'vue';

import data from '@/data.json';

const currentYear = new Date().toLocaleDateString('FR-fr', { year: 'numeric' });
const genders = ['féminin', 'masculin'];
const gender = ref(2);
const fullname = ref('ʕ ꈍܫꈍʔ'); // Ref from API maintenance : The API is beary tired ʕ ꈍܫꈍʔ. Scheduled reactivation: 23 August.

const setFullname = () => {
    fullname.value = null;

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
    <div class="w-full min-h-[100dvh] flex items-center justify-center text-center bg-image">
        <div
            class="flex flex-col items-center justify-center gap-6 max-w-sm mx-auto z-20 py-6 text-white"
        >
            <img src="@/assets/header.png" alt="" class="opacity-25" />
            <div class="text-xl font-semibold">
                Quel est ton nom kodan
                <select
                    name="gender"
                    id="gender"
                    v-model="gender"
                    class="rounded bg-white text-black py-1 px-1 text-lg cursor-pointer"
                    @change="setFullname"
                >
                    <option value="2">(aléatoire)</option>
                    <option v-for="(gender, g) in genders" :key="gender" :value="g">
                        {{ gender }}
                    </option></select
                >*&nbsp;?
            </div>
            <div class="italic text-xs -mt-4 text-gray-400">
                *&nbsp;Ne correspond pas à votre identité de genre, ni celle de votre personnage,
                mais au genre de nom et de son adjectif accordé que vous souhaitez.
            </div>
            <div
                class="text-3xl font-bold py-3 px-4 rounded-lg bg-white text-black inline-block"
                v-if="false"
            >
                <span
                    class="bg-gradient-to-t from-[#223073] to-[#519cc4] bg-clip-text text-transparent"
                >
                    {{ fullname }}
                </span>
            </div>
            <div class="text-3xl font-bold text-white">
                {{ fullname }}
            </div>
            <button
                v-if="gender !== ''"
                @click="setFullname"
                class="w-10 h-10 inline-flex items-center justify-center border-2 border-white hover:bg-white hover:bg-opacity-10 rounded-full aspect-square"
            >
                <svg
                    xmlns="http://www.w3.org/2000/svg"
                    width="24"
                    height="24"
                    viewBox="0 0 24 24"
                    fill="none"
                    stroke="currentColor"
                    stroke-width="2"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    class="icon icon-tabler icons-tabler-outline icon-tabler-reload"
                >
                    <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                    <path
                        d="M19.933 13.041a8 8 0 1 1 -9.925 -8.788c3.899 -1 7.935 1.007 9.425 4.747"
                    />
                    <path d="M20 4v5h-5" />
                </svg>
            </button>
            <img src="@/assets/footer.png" alt="" class="opacity-25" />
            <div class="text-sm flex gap-4 justify-center items-center">
                <div>Réalisé par <a href="https://thoanny.fr" target="_blank">Thoanny</a></div>
                <a href="https://thoanny.fr/t-potes" target="_blank">T-potes</a>
                <a href="https://github.com/thoanny/gw2-noms-kodans" target="_blank">Source</a>
            </div>
            <div class="text-xs opacity-50">
                © {{ currentYear }} ArenaNet, Inc. Tous droits réservés. NCsoft, le logo NC,
                ArenaNet, Arena.net, Guild Wars, Guild Wars Factions, Factions, Guild Wars
                Nightfall, Nightfall, Guild Wars: Eye of the North, Guild Wars Eye of the North, Eye
                of the North, Guild Wars 2 et tous les logos et dessins associés sont des marques
                commerciales et/ou déposées de NCsoft Corporation.
            </div>
        </div>
    </div>
</template>

<style scoped>
.bg-image {
    background: url('./assets/background.jpg') no-repeat center center;
    background-size: cover;
    background-attachment: fixed;
}

.bg-image:before {
    content: '';
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.66);
    position: fixed;
    top: 0;
    left: 0;
    z-index: 10;
}

h2 {
    @apply text-xl font-bold my-8;
}

a {
    @apply font-semibold;
}

a:hover {
    @apply underline;
}
</style>
