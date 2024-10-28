<template>
    <div>
        <h1>Federation Dashboard</h1>
        <p-button label="Add Player" @click="addPlayer" />
        <DataTable :value="players" responsiveLayout="scroll">
            <Column field="name" header="Name"></Column>
            <Column field="sport" header="Sport"></Column>
            <Column field="approved" header="Approval Status"></Column>
            <Column header="Actions" :body="actionTemplate"></Column>
        </DataTable>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    data() {
        return {
            players: []
        };
    },
    async created() {
        const response = await axios.get('/api/players');
        this.players = response.data;
    },
    methods: {
        addPlayer() {
            // Open modal to add player profile
        },
        actionTemplate(player) {
            return (
                <p-button label="Edit" @click={() => this.editPlayer(player)} />
            );
        }
    }
};
</script>
