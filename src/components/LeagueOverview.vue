<template>
    <div>
        <h3>{{ classicLeagueData.league.name }}</h3>
        <div class="league-table">
            <div v-for="team in classicLeagueData.new_entries.results" :key="team.entry" class="table-row">
                <span class="player-name">
                    [{{ team.player_first_name }}]
                </span>
                <span class="team-name">
                    {{ team.entry_name }}
                </span>
            </div>
        </div>
    </div>
</template>

<script setup>
import { onBeforeMount, onMounted, ref } from 'vue';
import { getClassicLeagues } from '../functions';

let classicLeagueData = ref(null)

const getClassicLeagueData = async () => {
    classicLeagueData.value = await getClassicLeagues()
}

onBeforeMount(async () => {
    await getClassicLeagueData()
})

onMounted(async () => {
})

</script>

<style lang="scss" scoped>
.league-table {
    display: flex;
    flex-direction: column;
}

.table-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 1rem;
}

.player-name, .team-name {
    display: inline;
}

.player-name {
    justify-self: right;
}

.team-name {
    justify-self: left;
}

</style>