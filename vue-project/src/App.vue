<script setup>
import { reactive } from 'vue';
const nome = "Matheus"

const novoObjeto = {
  nome: "Matheus",
  filmeFavorito: "Rocky"
}

function dizOla(nome) {
  return `${nome} diz oi`;
}

// imagens
const imagemArara = "link"
const imagemPraia = "link"

// bool
const botaoEstaDesabilitado = false
const gostaDoBatman = false
const gostaDoSuperman = false
const estaAutorizado = true

// Reactive -- Importe-o no início do código; 
const estado = reactive({
  contador: 0,
  email: '',
  saldo: 5000,
  transferindo: 0,
  nomes: ['gian', 'paulo', 'luisa', 'monica'],
  nomeAInserir: '',
})
function incrementar() {
  estado.contador++;
}
function decrementar() {
  estado.contador--;
}

function alteraEmail(evento) {
  estado.email = evento.target.value;
}

function mostraSaldoFuturo() {
  const { saldo, transferindo } = estado;
  return saldo - transferindo;
}

function validaValorDeTransferencia() {
  const { saldo, transferindo } = estado;
  return saldo >= transferindo;
}

function cadastraNome() {
  if (estado.nomeAInserir.legth >= 3) {
    estado.nomes.push(estado.nomeAInserir)
  } else {
    alert("Digite mais caracteres")
  }
}

</script>

<template>
  <h1>{{ dizOla("Pedro") }}</h1> <!-- {{  }} -- Mustaches (chaves), permitem importar diretamente do JS; -->
  <img v-if="gostaDoBatman" :src="imagemArara" alt="">
  <img v-else-if="gostaDoSuperman" :src="imagemPraia" alt="">
  <h2 v-else>Não curte heróis da DC</h2>

  <h1 v-if="estaAutorizado">Bem Vindo</h1>
  <h1 v-else>Não está autorizado</h1>

  <button :disabled="!botaoEstaDesabilitado">Enviar mensagem</button>

  <br>
  <hr>

  {{ estado.contador }}

  <button @click="incrementar" type="button">+</button>
  <button @click="decrementar" type="button">-</button>

  <br>
  <hr>

  {{ estado.email }}
  <input type="email" @keyup="alteraEmail">

  <br>
  <hr>

  Saldo: {{ estado.saldo }}
  <br>
  Transferindo: {{ estado.transferindo }}
  <br>
  Saldo depois da transferencia: {{ mostraSaldoFuturo() }}
  <br>
  <input class="campo" :class="{ invalido: !validaValorDeTransferencia() }" @keyup="evento => estado.transferindo = evento.target.value" type="number" placeholder="Quantia para transferir"/>
  <button v-if="validaValorDeTransferencia()">Transferir</button>
  <span v-else>Valor maior que o saldo</span>

  <br>
  <hr>

  <ul>
    <li v-for="nome in estado.nomes">
      {{ nome }}
    </li>
  </ul>
  <input @keyup="evento => estado.nomeAInserir = evento.target.value" type="text" placeholder="Digite um novo nome"/>
  <button @click="cadastraNome" type="button">Cadastrar nome</button>

  <h3 v-for="nome in estado.nomes">{{ nome }}</h3>

</template>

<style scoped>

img {
  max-width: 200px;
}

.invalido {
  outline-color: red;
  border-color: red;
}

.campo {
  border: 2px solid green;
}

</style>
