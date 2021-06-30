<template>
    <v-card class="card-container">
        <p class="conta"><v-icon class="icon" @click="$emit('return')" medium light left>{{svgConta}}</v-icon> Pagar um boleto</p>
        <p>Insira o código do boleto que quer pagar</p>
        <p>Saldo disponível em conta R$ {{ toMoney }}</p>
        <v-row class="justify-center">
          <v-col cols="8">
            <v-text-field
                v-model="codigoBoleto"
                :rules="codigoRules"
                :counter="37"
                label="Código de barras"
                required
            ></v-text-field>
          </v-col>
        </v-row>
        <v-row  v-if="pagar" class="justify-left">
          <v-col cols="8">
            <div class="pagar-container">
                <p><v-icon class="icon" small light left>{{icon}}</v-icon>Destino</p>
                <p>Nome: {{ this.boleto.nome }}</p>
                <p>CPF: {{ this.boleto.cpf }}</p>
                <p>Valor: R$ {{ parseFloat(this.boleto.valor).toFixed(2)  }}</p>
               
            </div>
          </v-col>
          <v-col cols="12">
            <v-btn
              elevation="2"
            >PAGAR
            </v-btn>
          </v-col>
        </v-row>

       

    </v-card>
</template>

<script>
import { mdiArrowLeft, mdiTooltipMinusOutline } from '@mdi/js';

export default {
  data () {
    return {
      svgConta: mdiArrowLeft,
      icon: mdiTooltipMinusOutline,
      codigoBoleto: '',
      pagar: false,
      cliente: 0,
      codigoRules: [
        v => !!v || 'Requer a inserção do código de barras',
        v => v.length <= 37 || 'Código deve ter pelo menos 47 carateres',
      ],
      boleto: {
        valor: 45.00, nome: "Roberto Emanuel Thiago Rezende", cpf: "054.XXX.895-00" 
        },
    }
  },
  props: ['amount'],
  computed: {
      toMoney: function() {
          return parseFloat(this.amount).toFixed(2)
      },
  },
  watch: {
    codigoBoleto: function() {
      if(this.codigoBoleto.length == 37) {
        this.pagar = true
      } else {
        this.pagar = false
      }
      if(this.codigoBoleto.length > 37) {
        this.codigoBoleto = this.codigoBoleto.substr(0, 36)
      }
    },
  },
  methods: {

  }
  
}
</script>

<style scoped>
.pagar-container {
  text-align: left;
  padding-left: 30px;
}

</style>
