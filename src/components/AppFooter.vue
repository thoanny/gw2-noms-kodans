<script setup>
const currentYear = new Date().toLocaleDateString('FR-fr', { year: 'numeric' });
</script>

<template>
    <img src="@/assets/footer.png" alt="" class="opacity-25" />
    <div class="text-xs flex gap-4 justify-center items-center">
        <div>
            Réalisé par <a href="https://thoanny.fr" target="_blank">Thoanny</a> pour
            <a href="https://lebusmagique.fr" target="_blank">Le Bus Magique</a>
        </div>
        <a href="https://thoanny.fr/t-potes" target="_blank">T-potes</a>
        <a href="https://github.com/thoanny/gw2-noms-kodans" target="_blank">Source</a>
    </div>
    <div class="text-xs opacity-50">
        © {{ currentYear }} ArenaNet, Inc. Tous droits réservés. NCsoft, le logo NC, ArenaNet,
        Arena.net, Guild Wars, Guild Wars Factions, Factions, Guild Wars Nightfall, Nightfall, Guild
        Wars: Eye of the North, Guild Wars Eye of the North, Eye of the North, Guild Wars 2 et tous
        les logos et dessins associés sont des marques commerciales et/ou déposées de NCsoft
        Corporation.
    </div>
</template>
