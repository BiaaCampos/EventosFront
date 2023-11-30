<!-- ModalExcluir.vue -->
<template>
    <div v-if="modalExclusaoVisivel" class="modal">
      <div class="modal-content">
        <span class="close" @click="fecharModalExclusao">&times;</span>
        <h2>Excluir Comprador</h2>
        <p>Tem certeza que deseja excluir este comprador?</p>
        <button class="btn btn-primary" @click="deletarComprador">Confirmar</button>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    props: {
      modalExclusaoVisivel: Boolean,
      compradorExclusao: Object,
      fecharModalExclusao: Function,
    },
    methods: {
      async deletarComprador() {
        try {
          console.log('Excluindo comprador...');
          await axios.delete(`https://localhost:7127/api/Comprador/${this.compradorExclusao.id}`);
  
          // Atualiza a lista de compradores após a exclusão
          alert("Comprador deletado com sucesso!!");
          window.location.reload(true);
          // const atualizacao = await axios.get('https://localhost:7127/api/Comprador');
          this.$emit('atualizarCompradores', atualizacao.data.$values);
          // Fecha o modal de exclusão
          this.fecharModalExclusao();
        } catch (error) {
          console.error('Erro na exclusão do comprador:', error);
        }
      },
    },
  };
  </script>
  

<style>

.modal {
  display: block;
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgba(0,0,0,0.4);
}

.modal-content {
  background-color: #fefefe;
  margin: 10% auto;
  padding: 20px;
  border: 1px solid #888;
  width: 20%;
  display: flex;
  justify-content: center;
}

.close {
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: red;
  text-decoration: none;
  cursor: pointer;
}

.btn-salvar{
    display: flex;
    justify-content: center;
    margin-top: 0.5em;
}


</style>