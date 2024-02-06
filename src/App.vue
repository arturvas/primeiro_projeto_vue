<script setup>
import { reactive } from "vue";

const nome = "artur";
const meuObjeto = {
  nome: "artur",
  filmeFavorito: "Interstelar",
};

function dizOla(nome) {
  return `${nome} diz oi`;
}

const imagemDoBatman =
  "https://images.bauerhosting.com/legacy/empire-tmdb/films/272/images/65JWXDCAfwHhJKnDwRnEgVB411X.jpg?ar=16%3A9&fit=crop&crop=top&auto=format&w=1440&q=80";

const imagemTomasMoreEoRei =
  "https://rainhastragicas.files.wordpress.com/2012/10/a-man-for-all-seasons.jpg?w=640";

const botaoEstaDesabilitado = false;

const mostrarImagemBatman = false;
const mostrarImagemTomasMores = false;

const estaAutorizado = false;

// let contador = 0;
const estado = reactive({
  contador: 0,
  email: "",
  saldo: 5000,
  transferindo: 0,
});

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
  // os {} significa que vamos extrair as propriedades
  const { saldo, transferindo } = estado;
  return saldo - transferindo;
}
</script>

<template>
  <h1>{{ dizOla("Artur") }}</h1>
  <img v-if="mostrarImagemBatman" :src="imagemDoBatman" alt="" />
  <img v-else-if="mostrarImagemTomasMores" :src="imagemTomasMoreEoRei" alt="" />
  <h2 v-else>Nao quer ver imagens</h2>

  <h1 v-if="estaAutorizado">Bem-vindo</h1>
  <h1 v-else>Não possui acesso</h1>

  <button :disabled="botaoEstaDesabilitado">enviar mensagem</button>

  <br />
  <hr />

  {{ estado.contador }}

  <button @click="incrementar" type="button">+</button>
  <button @click="decrementar" type="button">-</button>

  <br />
  <hr />

  {{ estado.email }}
  <input type="email" @keyup="alteraEmail" />
  <!-- 
    @keyup = insere o conteudo instantaneamente 
    @change = insere o conteudo somente apos sair do campo
  -->

  <br />
  <hr />

  Saldo: {{ estado.saldo }} <br />
  Transferirindo: {{ estado.transferindo }} <br />
  Saldo depois da trasnferencias: {{ mostraSaldoFuturo() }} <br />
  <input
    :class="{ invalido: estado.transferindo > estado.saldo }"
    @keyup="(evento) => (estado.transferindo = evento.target.value)"
    type="number"
    placeholder="Quantia para transferir"
  />
</template>

<style scoped>
img {
  max-width: 200px;
}

.invalido {
  outline: 2px solid tomato;
  /* border: 2px solid red; */
}
</style>
