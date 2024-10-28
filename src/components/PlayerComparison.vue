<template>
    <div>
        <h1>Compare Players</h1>
        <p-dropdown
            :options="players"
            optionLabel="name"
            placeholder="Select Player 1"
            v-model="player1"
        />
        <p-dropdown
            :options="players"
            optionLabel="name"
            placeholder="Select Player 2"
            v-model="player2"
        />
        <div v-if="player1 && player2">
            <h2>Comparison</h2>
            <div>
                <p><strong>{{ player1.name }}</strong> vs <strong>{{ player2.name }}</strong></p>
                <p><strong>Achievements:</strong> {{ player1.achievements }} vs {{ player2.achievements }}</p>
                <p><strong>Records:</strong> {{ player1.records }} vs {{ player2.records }}</p>
                <p><strong>History:</strong> {{ player1.history }} vs {{ player2.history }}</p>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    data() {
        return {
            players: [],
            player1: null,
            player2: null
        };
    },
    async created() {
        const response = await axios.get('/api/players');
        this.players = response.data;
    }
};
</script>
