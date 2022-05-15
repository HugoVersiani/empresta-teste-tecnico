<template>
  <main>
    <form @submit.prevent="enviar">
         <label for="valor">Valor:</label>
        <input v-model="dados.valor" id="valor" type="text" name="valor"/>
        
        <label for="instituicao">Instituição:</label>
         <select v-model="dados.instituicao" id="instituicao" name="instituicao">
            <option v-for="(instituicoes, index) in (instituicoes)" :key="index" :value="instituicoes.chave">{{instituicoes.valor}}</option>
        </select>
         <label for="convenio">Convênio:</label>
        <select v-model="dados.convenio" id="convenio" name="convenio">
            <option v-for="(convenios, index) in (convenios)" :key="index" :value="convenios.chave">{{convenios.valor}}</option>
        </select>
         <label for="parcelas">Parcelas:</label>
        <select v-model="dados.parcelas" name="parcelas">
            <option value="36">36</option>
            <option value="40">40</option>
            <option value="60">60</option>
            <option value="72">72</option>
            <option value="84">84</option>
        </select>
        <button type="submit">Simular</button>
    </form>
  </main>
</template>
<script>

import api from '@/services/api.js';

export default {
  name: "Home",

  data() {
      return {
          dados: {
            valor_emprestimo: "",
            instituicoes: [],
            convenios: [],
            parcela: ""

          },
        
          parcelas: "",
          instituicoes: [],
          convenios: []
      }
  },
  mounted() {
      api.get('/instituicao').then(response => {
          this.instituicoes = response.data;
      });
      api.get('/convenio').then(response => {
          this.convenios = response.data;
      })
  },
  methods: {
      enviar() {
         api.post('/simular', this.dados).then(response => {
           alert(response.data);
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
}

form {
  width: 100%;
  background-color: #fff;
  margin: 20px auto;
  display: flex;
  flex-direction: column;
  align-items: center;


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

button:hover {
    background-color: #c45800;
}
</style>