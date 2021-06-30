<template>
  <v-container id="app">
    <div class="header">
      <p>Olá, Daniel Soares</p>
      <p>Agência: 0001 Conta 60538591-7</p>
      <p>Banco 590 - Capgemini S.A.</p>
    </div>
    <v-row class="justify-center">
      <v-col cols="6" class="mx-auto">
        <Conta v-if="menuSelected == 0" :amount="user.amount"/>
        <Pagar v-if="menuSelected == 1" :amount="user.amount" @return="setMenuSelected(0)"/>
        <Pix v-if="menuSelected == 2" :amount="user.amount" @return="setMenuSelected(0)"/>
        <Transferir v-if="menuSelected == 3" :amount="user.amount" @return="setMenuSelected(0)"/>
        <Depositar v-if="menuSelected == 4" :amount="user.amount" @return="setMenuSelected(0)"/>
      </v-col>
    </v-row>
   <div class="footer">
    <v-row justify="space-around">
     <v-col v-for="(action, index) in actions" :key="index">
      <button class="button"  @click="setMenuSelected(action.value)">
        <v-icon class="icon"      
        large
        light
        left
        >{{action.icon}}</v-icon>
        <p>{{action.name}}</p>
      </button>
     </v-col>  
    </v-row>
   </div>
  </v-container>
</template>

<script>
import { mdiWalletPlusOutline,
 mdiTooltipMinusOutline, 
 mdiSync,
 mdiScatterPlotOutline,
 mdiWalletOutline } from '@mdi/js'
import Conta from '@/components/Conta'
import Pagar from '@/components/Pagar'
import Pix from '@/components/Pix'
import Transferir from '@/components/Transferir'
import Depositar from '@/components/Depositar'

export default {
  name: 'App',
  components: {
    Conta,
    Pagar,
    Pix,
    Transferir,
    Depositar
  },
  data () {
    return {
      actions: [
        {name: "Pagar", icon: mdiTooltipMinusOutline, value: 1},
        {name: "Pix", icon: mdiScatterPlotOutline, value: 2 },
        {name: "Transferir", icon: mdiSync, value: 3},
        {name: "Depositar", icon: mdiWalletPlusOutline, value: 4},
      ],
      user: {
        amount: 50.00
      },
      menuSelected: 0,
      svgConta: mdiWalletOutline
    }
  },
  methods: {
    setMenuSelected(value) {
      this.menuSelected = value;
    },
  }
}
</script>

<style>
body {
    background-color: #01260E;

}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #fff;
  background-color: #01260E;
  margin-top: 60px;
}

.button {
  background-color: #fff;
  border-radius: 20px;
  color: rgb(61, 59, 59);
  padding-top: 30px;
  padding-bottom: 45px;
  width: 100%;
  transition: top 1s;
}

.button:hover{
  box-shadow: 0px 0px 16px #000;
  position: relative;
  top: -10px;
}

.button p{
  margin-top: 15px;
  font-weight: 600;
}

.justify-center {
  display: flex;
  justify-content: center;
}

.card-container {
  margin-top: 20px;
  margin-bottom: 35px;
  padding-top: 35px;
  padding-bottom: 45px;
  
}

.card-container .conta{
  text-align: left;
  position: relative;
  top: -15px;
  left: 15px;
}

.card-container h1{
  color: rgb(61, 59, 59);
  font-weight: 800;
  font-size: 40px;
}

.card-container p{
  color: rgb(61, 59, 59);
  font-weight: 600;
}
</style>
