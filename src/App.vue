<template>
  <div id="app">
      <!-- Inicialização do componente do título da página -->
      <Menu/>
    <div class="container" id="div_repos">
        <div class="card card-body">
          <!-- Um h3 para servir de label para localizar usuário -->
          <h3>Pesquisar Usuário:</h3>
          <input v-model="dd.use" name="usu" type="text" id="search" class="form-control" required>
        </div>
        <div class="row mt-0">
          <div class="col-md-4">
              <!-- Inicialização do componente com dados do repositório do cliente  -->
              <DadosCliente :user='user'/>
                <button id="botao" v-on:click="getUser">Localizar</button>
                <button id="botao" v-on:click="atualizar">Limpar Dados</button>
          </div>
          <div class="col-md-6">
            <!-- Inicialização do componente com os repositórios -->
            <Repositorio v-for="rps in repositorio" :key='rps' :repositorio='rps'/>
          </div>
        </div>
    </div>
  </div>
</template>

<script>

//Importação dos componentes e da biblioteca axios
import Menu from './components/Menu';
import DadosCliente from './components/DadosCliente';
import Repositorio from './components/Repositorio';
import axios from 'axios'

export default {
  name: 'App',
  data(){
    return{
      //Inicializando as credenciais do git
      dadosGit:{
        url: 'https://api.github.com/users',
        id: '17248991',
        chave: 'MDQ6VXNlcjM4ODExNjIz'
      },
      // Inicialização de uma lista que receberá o data da função axios.get
      user:[],
      repositorio: [],
      erros:[],
      dd: {use: '',
      },
   
    }
  },
  //Declaração dos componentes
  components: {
    Menu,
    DadosCliente,
    Repositorio
    
  },
  //Método para acessar api do git e receber os dados do repocitório
  methods:{
    getUser(){
          const {url,id,chave,count,sort} = this.dadosGit;

      axios.get(`${url}/${this.dd.use}?client_id=${id}&client_secret=${chave}`)
      .then(({data}) => (this.user = data)).catch((e) => (this.erros.push(e)));
     
      this.validarErros()

      axios.get(
        `${url}/${this.dd.use}/repos?per_page=${count}&sort=${sort}&client_id=${id}&client_secret=${chave}`
      ).then(({data}) => (this.repositorio = data))

    },

    //Método para validar erro de usuário não localizado
    validarErros: function msgError(){
      if(this.erros.length > 0){
        alert('Usuário Inválido')
        document.getElementById('search').value = ''
        this.erros = []
        
      }
    },

    //Método para dar um refresh no sistema
    atualizar: function refreshPage(){
      window.location.reload()
      this.user = []
    }
  }
}

</script>

<style>
  /* Formatar o botão localizar e limpar */
  #botao{
    width:200px;  
    height:25px;
    margin-top: 5px;
    text-align:center;	
    color:#999;
    background: #003366;
  }

</style>
