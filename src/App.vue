<script setup>
import { reactive } from 'vue';

const nome = 'Bira Neves';
const meuObjeto = {
    nome: 'Bira',
    filmeFavorito: 'Vingadores',
};

function dizOla(nome) {
    return `${nome} diz oi!`;
}

const imagemBatman = 'https://th.bing.com/th/id/OIP.Ep0LNE3teOH7x0Kl3JxLNgHaEo?w=296&h=185&c=7&r=0&o=5&pid=1.7';
const imagemSuperman = 'https://th.bing.com/th/id/OIP.pNH4MLNW03V8rCAsTIAj7wHaEK?w=322&h=181&c=7&r=0&o=5&pid=1.7';
const botaoEstaDesabilitado = false;
const gostaDoBatman = false;
const gostaDoSuperman = false;
const estaAutorizado = false;

const estado = reactive({
    contador: 0,
    email: '',
    saldo: 5000,
    transferindo: 0,
});

function incrementar() {
    estado.contador++;
}

function decrementar() {
    estado.contador--;
}

function alteraEmail(e) {
    estado.email = e.target.value;
}

function mostraSaldoFuturo() {
    const { saldo, transferindo } = estado;
    return saldo - transferindo;
}
</script>

<template>
    <h1>{{ dizOla('Bira') }}</h1>
    <img v-if="gostaDoBatman" :src="imagemBatman" alt="" />
    <img v-else-if="gostaDoSuperman" :src="imagemSuperman" alt="" />
    <h2 v-else>Não curte heróis da DC.</h2>

    <h1 v-if="estaAutorizado">Bem-vindo!</h1>
    <h1 v-else>Não possui acesso.</h1>

    <button :disabled="botaoEstaDesabilitado">Enviar mensagem</button>

    <br />
    <hr />

    {{ estado.contador }}

    <button @click="incrementar" type="button">+</button>
    <button @click="decrementar" type="button">-</button>

    <br />
    <hr />

    {{ estado.email }}
    <input type="email" @keyup="alteraEmail" />

    <br />
    <hr />

    Saldo: {{ estado.saldo }}<br />
    Transferindo: {{ estado.transferindo }}<br />
    Saldo depois da transferência: {{ mostraSaldoFuturo() }}<br />
    <input @keyup="e => (estado.transferindo = e.target.value)" type="number" placeholder="Quantia a transferir" />
</template>

<style scoped></style>
