<script setup>
import {reactive} from 'vue';

// Objeto principal para acesso de infos
const objeto = {
  nome: 'Igor',
  idade: 28,
  email: 'igor@example.com',
  telefone: '(11) 99999-9999',
  
};

// Verifica qual personagem você gosta e exibe a foto correspondente
const coringa = "https://ingresso-a.akamaihd.net/b2b/production/uploads/articles-content/041f7cd8-63e8-4645-8284-21cf86d332c6.jpg";
const narizinho = 'https://vejasp.abril.com.br/wp-content/uploads/2016/12/izak-dahora-o-saci-e-isabelle-drummond-a-boneca-emilia-personagens-do-programa-infantil-sitio-do-picapau-amarelo-da-tv-globo.jpeg?quality=70&strip=info&w=650'
const botaoEstaDesabilitado = true;
 //Controle as opções de fotos
  const gostaDoCoringa = false;
  const gostaDoNarizinho = false;
  const estaAutorizado = true;

  // Outra forma de printar com uma função
  function dizOI(nome){
    return `${nome} diz oi`
  }
// Referente ao contador de numeros
  function incrementar(){
    estado.contador++;
    console.log(contador);
  }
  function decrementar(){
    estado.contador--;
    console.log(contador);
  }

  let contador = 0;
  const estado = reactive({
    contador: 0,
    email: '',
    saldo: 5000,
    transferindo: 0,
    nomes: ['Igor', 'Lorenzzo', 'Fernanda', 'Francisca', 'Joaquina'],
    cadastrarNome: '',
  })

  // Escreve acima do campo e-mail o que esta escrito no input
  function alteraEmail(e){
  estado.email = e.target.value
  }

  // Calcula o saldo futuro de acordo com o saldo e a transferencia
  function mostraSaldoFuturo(){ 
    const {saldo, transferindo} = estado;
    return saldo - transferindo
  }
  // Verifica se há saldo para a transferência
  function validaTransferencia(){
    const {saldo,transferindo}= estado;
    return saldo >= transferindo;
  }
 //Cadastra o nome se houver no minimo 3 caracteres
  function salvaNome(){
    if(estado.cadastrarNome.length >= 3){
      estado.nomes.push(estado.cadastrarNome)
    }else{
      alert('Digite mais caracteres')
    }
  }
</script>

<template>
<h1>{{ dizOI('Paulo') }}</h1>
<img v-if="gostaDoCoringa" :src="coringa" alt="">
<img v-else-if="gostaDoNarizinho" :src="narizinho" alt="">

<h2 v-else>Não curte nada </h2>

<h1 v-if="estaAutorizado">Bem-vindo</h1>
<h1 v-else="!estaAutorizado">Não possui acesso</h1>

<button :disabled="botaoEstaDesabilitado">Enviar Mensagem</button>

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
Saldo: {{ estado.saldo }} <br>
Transferindo: {{ estado.transferindo }} <br>
Saldo pós transferência: {{ mostraSaldoFuturo() }} <br>
<input :class="{invalido: !validaTransferencia()}" @keyup="e=>estado.transferindo = e.target.value" type="number" placeholder="Quantia a transferir">
<button v-if="validaTransferencia()">Transferir</button>
<span v-else>Valor maior que o saldo</span>

<br>
<hr>
<ul>
  <li v-for="nome in estado.nomes">
    {{ nome }}
  </li>
</ul>

<input @keyup="e=>estado.cadastrarNome = e.target.value" type="text" placeholder="Digite um novo nome">
<button @click="salvaNome" type="button">Cadastrar</button>

<h3 v-for="nome in estado.nomes">{{ nome }}</h3>

</template>
<style scoped>
img{
  max-width: 200px;
}

.invalido{
  outline-color:red;
  color: red;
}
</style>
