<template>
  <div>
    <h2>Transferências agendadas</h2>
    <ul>
      <li v-for="transfer in transfers" :key="transfer.id">
        {{ transfer.sourceAccount }} to {{ transfer.destinationAccount }} - ${{ transfer.amount }} on {{ transfer.transferDate }} (Fee: ${{ transfer.fee }})
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      transfers: []
    };
  },
  async created() {
    try {
      const response = await axios.get('http://localhost:8080/transfers');
      this.transfers = response.data;
    } catch (error) {
      alert('Failed to fetch transfers: ' + error.response.data.message);
    }
  }
};
</script>
