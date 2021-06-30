<template>
    <v-card class="card-container">
        <p class="conta"><v-icon class="icon" @click="$emit('return')" medium light left>{{svgConta}}</v-icon> Tranferência</p>
        <p>Qual é o valor da transferência?</p>
        <p>Saldo disponível em conta R$ {{ toMoney }}</p>
        <v-row class="justify-center">
          <v-col cols="8">
            <v-text-field
                v-model="valorPix"
                label="R$ 0,00"
                required
            ></v-text-field>
          </v-col>
          <v-col  v-if="pagar" cols="8">
            <v-text-field
                v-model="chave"
                label="Nome, CPF/CNPJ ou chave Pix"
                required
            ></v-text-field>
          </v-col>
          <v-col v-if="chavePix" cols="12">
            <v-btn
              elevation="2"
            >Transferir
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
      valorPix: '',
      chave: '',
      chavePix: ''
    }
  },
  props: ['amount'],
  computed: {
      toMoney: function() {
          return parseFloat(this.amount).toFixed(2)
      }
  },
  watch: {
    valorPix: function() {
      if(this.valorPix > 0) {
        this.pagar = true
      } else {
        this.pagar = false
      }
    },
    chave: function() {
      if(this.chave.length > 0) {
        this.chavePix = true
      } else {
        this.chavePix = false
      }
    },
  },
  methods: {

  }
  
}
</script>

<style scoped>

</style>
