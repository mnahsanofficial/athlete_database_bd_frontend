<template>
    <div>
        <h1>Player Profiles</h1>
        <p-dropdown
            :options="federations"
            optionLabel="name"
            placeholder="Select Federation"
            v-model="selectedFederation"
            @change="filterPlayers"
        />
        <DataTable :value="players" responsiveLayout="scroll">
            <Column field="name" header="Name"></Column>
            <Column field="sport" header="Sport"></Column>
            <Column field="achievements" header="Achievements"></Column>
        </DataTable>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    data() {
        return {
            federations: [],
            selectedFederation: null,
            players: []
        };
    },
    async created() {
        const federationResponse = await axios.get('/api/federations');
        this.federations = federationResponse.data;

        const playerResponse = await axios.get('/api/players');
        this.players = playerResponse.data;
    },
    methods: {
        filterPlayers() {
            this.players = this.players.filter(
                player => player.federation === this.selectedFederation
            );
        }
    }
};
</script>
