<template>
    <div>
        <h1>Super Admin Dashboard</h1>
        <DataTable :value="players" responsiveLayout="scroll">
            <Column field="name" header="Name"></Column>
            <Column field="sport" header="Sport"></Column>
            <Column field="federation" header="Federation"></Column>
            <Column field="approved" header="Approval Status"></Column>
            <Column header="Actions" :body="approvalTemplate"></Column>
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
        approvePlayer(playerId) {
            axios.patch(`/api/players/${playerId}/`, { approved: true });
        },
        approvalTemplate(player) {
            return (
                <p-button
                    label="Approve"
                    v-if="!player.approved"
                    @click={() => this.approvePlayer(player.id)}
                />
            );
        }
    }
};
</script>
