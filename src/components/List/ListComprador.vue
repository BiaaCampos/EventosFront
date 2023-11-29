<!-- CompradorList.vue -->
<template>
  <div class="app">
    <div class="container">
      <p class="Login">Visualizar Compradores</p>
      <!-- Tabela de Compradores -->
      <table class="table">
        <thead>
          <tr>
            <th scope="col">#</th>
            <th scope="col">Nome</th>
            <th scope="col">Sobrenome</th>
            <th scope="col">Email</th>
            <th scope="col">RA</th>
            <th scope="col">Ativo</th>
            <th scope="col">Ações</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(comprador, index) in compradores" :key="index">
            <th scope="row">{{ index + 1 }}</th>
            <td>{{ comprador.nome }}</td>
            <td>{{ comprador.sobrenome }}</td>
            <td>{{ comprador.email }}</td>
            <td>{{ comprador.ra }}</td>
            <td>{{ comprador.checkbox ? 'Ativo' : 'Inativo' }}</td>
            <td>
              <button class="btn btn-primary btn-editar-excluir" @click="abrirModalEdicao(comprador)">Editar</button>
              <button class="btn btn-danger btn-editar-excluir" @click="abrirModalExclusao(comprador)">Excluir</button>
            </td>
          </tr>
        </tbody>
      </table>
      <div class="botao">
        <a class="btn btn-primary btn-visu" href="/CadComprador" role="button">Cadastrar Comprador</a>
      </div>

      <!-- ModalEditar component -->
      <ModalEditar
        :modalVisivel="modalVisivel"
        :compradorEditado="compradorEditado"
        :fecharModal="fecharModal"
        @edicaoConcluida="atualizarCompradores"
      />
      
      <!-- ModalExcluir component -->
      <ModalExcluir
        :modalExclusaoVisivel="modalExclusaoVisivel"
        :compradorExclusao="compradorExclusao"
        :fecharModalExclusao="fecharModalExclusao"
        @atualizarCompradores="atualizarCompradores"
      />
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import ModalEditar from '../Modal/ModalEditar.vue';
import ModalExcluir from '../Modal/ModalExcluir.vue';

export default {
  components: {
    ModalEditar,
    ModalExcluir,
  },
  setup() {
    const compradores = ref([]);
    const modalVisivel = ref(false);
    const compradorEditado = ref({});
    const modalExclusaoVisivel = ref(false);
    const compradorExclusao = ref({});

    onMounted(async () => {
      try {
        const response = await axios.get('https://localhost:7127/api/Comprador');
        compradores.value = response.data.$values;
        console.log(compradores.value);
      } catch (error) {
        console.error('Erro na solicitação:', error);
      }
    });

    const abrirModalEdicao = (comprador) => {
      compradorEditado.value = { ...comprador };
      modalVisivel.value = true;
    };

    const abrirModalExclusao = (comprador) => {
      compradorExclusao.value = { ...comprador };
      modalExclusaoVisivel.value = true;
    };

    const fecharModal = () => {
      modalVisivel.value = false;
    };

    const fecharModalExclusao = () => {
      modalExclusaoVisivel.value = false;
    };

    const atualizarCompradores = async () => {
      try {
        compradores.value = await axios.get('https://localhost:7127/api/Comprador').then(response => response.data.$values);
      } catch (error) {
        console.error('Erro ao atualizar lista de compradores:', error);
      }
    };

    return {
      compradores,
      modalVisivel,
      compradorEditado,
      modalExclusaoVisivel,
      compradorExclusao,
      abrirModalEdicao,
      abrirModalExclusao,
      fecharModal,
      fecharModalExclusao,
      atualizarCompradores,
    };
  },
};
</script>



<style scoped>
@import url('https://fonts.cdnfonts.com/css/lexend-deca');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family:'Lexend Deca', sans-serif;
}

.btn-editar-excluir{
  padding: 4px;
  margin-left: 0.5em;
}

.app{
  display: flex;
  justify-content: center;
  margin-top: 2em;
}

.Login{
  font-size: 25px;
  display: flex;
  justify-content: center;
  text-transform: uppercase;
  margin-bottom: 1em;
  text-decoration: underline;
}

.botao{
  display: flex;
  justify-content: center;
  margin-top: 2em;
}

.btn-visu{
  padding: 5px 25px;
  background-color: transparent;
  color: black;
  border-color: black;
}

.btn-visu:hover{
  padding: 5px 25px;
  background-color: #003264;
  color: white;
  border-color: white;
}



</style>
