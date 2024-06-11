<template>
  <div>
    <h2>Histórico de transferências agendadas</h2>
    <div class="table-responsive">
      <table class="transfers-table">
        <thead>
          <tr>
            <th>Conta de origem</th>
            <th>Conta de destino</th>
            <th>Quantia</th>
            <th>Data de transferência</th>
            <th>Taxa</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="transfer in transfers" :key="transfer.id">
            <td>{{ transfer.sourceAccount }}</td>
            <td>{{ transfer.destinationAccount }}</td>
            <td>${{ transfer.amount }}</td>
            <td>{{ transfer.transferDate }}</td>
            <td>${{ transfer.fee }}</td>
          </tr>
        </tbody>
      </table>
    </div>
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

<style>
.transfers-table {
  width: 100%;
  border-collapse: collapse;
}

.transfers-table th, .transfers-table td {
  padding: 8px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}

.transfers-table th {
  background-color: #f2f2f2;
}

/* Responsive Styles */
.table-responsive {
  overflow-x: auto;
  max-width: 100%;
  margin-bottom: 15px;
}

@media (max-width: 768px) {
  .transfers-table th, .transfers-table td {
    padding: 5px;
  }
}
</style>
