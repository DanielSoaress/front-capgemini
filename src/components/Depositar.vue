<template>
    <v-card class="card-container">
        <p class="conta"><v-icon class="icon" @click="$emit('return')" medium light left>{{svgConta}}</v-icon> Depositar</p>
        <p>Qual é o valor do depósito?</p>
        <p>Saldo disponível em conta R$ {{ toMoney }}</p>
        <v-row class="justify-center">
          <v-col cols="8">
            <v-text-field
                v-model="valor"
                label="R$ 0,00"
                required
            ></v-text-field>
          </v-col>
          <v-col v-if="pagar" cols="12">
            <v-btn
              elevation="2"
            >Depositar
            </v-btn>
          </v-col>
        </v-row>
    </v-card>
</template>

<script>
import { mdiArrowLeft } from '@mdi/js';

export default {
  data () {
    return {
      svgConta: mdiArrowLeft,
      valor: '',
      pagar: false,
    }
  },
  props: ['amount'],
  computed: {
      toMoney: function() {
          return parseFloat(this.amount).toFixed(2)
      }
  },
  watch: {
    valor: function() {
      if(this.valor > 0) {
        this.pagar = true
      } else {
        this.pagar = false
      }
    },
  },
  methods: {

  }
  
}
</script>

<style scoped>

</style>
