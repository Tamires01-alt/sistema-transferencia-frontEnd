<template>
  <div>
    <h2>Agendar transferência</h2>
    <form @submit.prevent="scheduleTransfer">
      <div>
        <label for="sourceAccount">Conta de origem:</label>
        <input type="text" v-model="transfer.sourceAccount" id="sourceAccount" />
      </div>
      <div>
        <label for="destinationAccount">Conta de destino:</label>
        <input type="text" v-model="transfer.destinationAccount" id="destinationAccount" />
      </div>
      <div>
        <label for="amount">Quantia:</label>
        <input type="number" v-model="transfer.amount" id="amount" />
      </div>
      <div>
        <label for="transferDate">Data de transferência:</label>
        <input type="date" v-model="transfer.transferDate" id="transferDate" />
      </div>
      <button type="submit">Agendar transferência</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      transfer: {
        sourceAccount: '',
        destinationAccount: '',
        amount: '',
        transferDate: ''
      }
    };
  },
  methods: {
    async scheduleTransfer() {
    try {
        await axios.post('http://localhost:8080/transfers', this.transfer);
        alert('Transferência agendada com sucesso!');
        this.transfer = { sourceAccount: '', destinationAccount: '', amount: '', transferDate: '' };
    } catch (error) {
        if (error.response && error.response.data && error.response.data.message) {
        alert('Falha ao agendar transferência: ' + error.response.data.message);
        } else {
        alert('Falha ao agendar a transferência. ' + error.message);
        }
    }
    }
  }
};
</script>
