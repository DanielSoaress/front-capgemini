<template>
    <v-card class="card-container">
        <p class="conta"><v-icon class="icon" large light left>{{svgConta}}</v-icon> Conta</p>
        <p>Saldo disponível</p>
        <h1>R$ {{toMoney}}</h1>
    </v-card>
</template>

<script>
import { mdiWalletOutline } from '@mdi/js'

export default {
  data () {
    return {
      svgConta: mdiWalletOutline
    }
  },
  props: ['amount'],
  computed: {
      toMoney: function() {
          return parseFloat(this.amount).toFixed(2)
      }
  }
  
}
</script>

<style scoped>

</style>
