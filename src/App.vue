<template>
  <div id="app">
    <TransferForm />
    <TransferList />
  </div>
</template>

<script>
import TransferForm from './components/TransferForm.vue';
import TransferList from './components/TransferList.vue';

export default {
  components: {
    TransferForm,
    TransferList
  }
};
</script>
