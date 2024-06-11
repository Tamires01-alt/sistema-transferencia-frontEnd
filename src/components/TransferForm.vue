<template>
  <div style="border-style: inset; width: 500px; padding: 20px 20px 20px 20px; display: flex; justify-content: center; background-color: #f5f5f5">
    <h2>Agende sua transferência</h2>
    <form @submit.prevent="scheduleTransfer">
      <div style="  padding : 10px;;">
        <label for="sourceAccount" class="titleTextForm">Conta de origem:</label>
        <input style="width: 200px; heigth: 90px; "  type="text" v-model="transfer.sourceAccount" id="sourceAccount" />
      </div>
      <div class="inputValueForm">
        <label for="destinationAccount" class="titleTextForm">Conta de destino:</label>
        <input style="width: 200px; heigth: 90px; gap: 10px;" type="text" v-model="transfer.destinationAccount" id="destinationAccount" />
      </div>
      <div class="inputValueForm">
        <label for="amount" class="titleTextForm">Valor:</label>
        <input style="width: 200px; heigth: 90px;" type="number" v-model="transfer.amount" id="amount" />
      </div>
      <div class="inputValueForm">
        <label for="transferDate" class="titleTextForm">Data de transferência:</label>
        <input style="width: 200px; heigth: 90px;" type="date" v-model="transfer.transferDate" id="transferDate" />
      </div>
      <div style="padding: 10px 10px 0px 30px">
        <button class="buttonTranfer"  type="submit">Agendar transferência</button>
      </div>
      
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
<style >
.inputValueForm {
    display: flex; 
    flex-direction: column; 
    padding : 10px;
}

.buttonTranfer{
    padding: 10px 10px 10px 10px;
    color: black;
    background-color: chartreuse;
    border: none;
    border-radius: 10px;
    cursor: pointer;
}
.titleTextForm{
    font-size: 20px;
    margin-bottom: 2px;
    color: black;
}
</style>
