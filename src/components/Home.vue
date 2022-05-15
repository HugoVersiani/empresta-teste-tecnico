<template>
  <main>

    <form @submit.prevent="enviar">
         <label for="valor">Valor:</label>
        <input v-model="dados.valor_emprestimo" id="valor" type="number" name="valor"/>
        
        <label for="instituicao">Instituição:</label>
         <select multiple v-model="dados.instituicoes" id="instituicao" name="instituicao">
            <option v-for="(instituicao, index) in (instituicao)" :key="index" :value="instituicao.chave">{{instituicao.valor}}</option>
        </select>
         <label for="convenio">Convênio:</label>
        <select multiple v-model="dados.convenios" id="convenio" name="convenio">
            <option v-for="(convenio, index) in (convenio)" :key="index" :value="convenio.chave">{{convenio.valor}}</option>
        </select>
         <label for="parcelas">Parcelas:</label>
        <select v-model="dados.parcela" name="parcelas">
            <option value=36>36</option>
            <option value=40>40</option>
            <option value=60>60</option>
            <option value=72>72</option>
            <option value=84>84</option>
        </select>
        <button type="submit">Simular</button>
    </form>
    
    <div class="popup">
      <div v-for="(simulacao, index) in (simulacao)" :key="index">
        <h2>{{index}}</h2>
        <span class="valor">R$ {{dados.valor_emprestimo}}</span>
      
          <div class="conteudo-simulacao" v-for="(simulacao, index) in (simulacao)" :key="index">
            <span v-if="dados.parcela <= simulacao.parcelas">
            {{simulacao.parcelas}} parcelas de R$ {{simulacao.valor_parcela}} <br>
            </span>
            <span v-if="dados.parcela <= simulacao.parcelas">Taxa de juros: {{simulacao.taxa}}</span>
          </div>
          
      </div>
    </div>
  </main>
</template>
<script>

import api from '@/services/api.js';

export default {
  name: "Home",

  data() {
      return {
          simulacao: [],

          dados: {
            valor_emprestimo: '',
            instituicoes:[] ,
            convenios: [],
            parcela: '',
      
          },
        
          parcelas: "",
          instituicao: [],
          convenio: []
      }
  },
  mounted() {
      api.get('/instituicao').then(response => {
          this.instituicao = response.data;
      });
      api.get('/convenio').then(response => {
          this.convenio = response.data;
      })
  },
  methods: {
      enviar() {
        this.dados.parcela = parseInt(this.dados.parcela)
        const dados  = this.dados
         api.post('/simular', { valor_emprestimo: dados.valor_emprestimo,
                                instituicoes: dados.instituicoes,
                                convenios: dados.convenios,
    parcela: 60}).then(response => {
         this.simulacao = response.data;
        
         })
      }
  }

};
</script>
<style scoped>
main {
  width: 100%;
  height: calc(100vh - 95px);
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

form {
  width: 100%;
  background-color: #fff;
  margin: 20px auto;
  display: flex;
  flex-direction: column;
  align-items: center;


}
form label {
    display: flex;
    width: 50%;
    align-items: flex-start;
    padding-top: 10px;

}

form input, select {
    padding: 10px;
    margin: 10px;
    width: 50%;
    border-radius: 5px;
    border: 1px solid rgb(197, 197, 197);
}

button {
    cursor: pointer;
    padding: 10px 20px;
    margin: 10px;
    background-color: var(--color-primary);
    border-radius: 5px;
    border: none;
    color: #fff;
    font-size: 1em;
    box-shadow: 0 6px 21px -3px rgb(239 108 0 / 50%);
    transition: 0.15s ease-in-out,
}

h2 {
  color: var(--color-secondary);
  font-size: 1.8em;
  padding: 10px 0;
}

.valor {
  color: rgb(167, 167, 167);
  font-size: 1.6em;
  font-weight: bold;
}

button:hover {
    background-color: #c45800;
}

.popup {
  width: 50%;
  height: 500px;
  border:1px solid var(--color-primary);
  border-radius: 10px;
  margin-bottom: 50px;
  overflow-y: scroll;
  padding: 30px
  
}
.conteudo-simulacao {
  background-color: rgb(241, 241, 241);
  padding: 10px 10px;
  margin: 10px 0;
  border-radius: 5px;
}
.conteudo-simulacao span {
  margin: 12px 0;
  color: rgb(56, 56, 56);
 
}

.conteudo-simulacao span:first-child {
  font-weight: bold;
  font-size: 1.4em;
  margin-bottom: 10px;
}

.conteudo-simulacao span:last-child {
  margin: 12px 0;
}
@media (max-width: 1024px) {
  form input, select {
    width: 90%;
  }

  .popup {
    width: 90%;
  }

  form label {
    display: flex;
    width: 90%;
    align-items: flex-start;
    padding-top: 10px;

}
}

</style>