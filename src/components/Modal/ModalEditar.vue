<!-- ModalEditar.vue -->
<template>
    <div v-if="modalVisivel" class="modal">
      <div class="modal-content">
        <span class="close" @click="fecharModal">&times;</span>
        <h2>Editar Comprador</h2>
        <form @submit.prevent="salvarEdicao">
          <div class="form-group">
            <label for="editNome">Nome:</label>
            <input v-model="compradorEditado.nome" id="editNome" class="form-control" placeholder="Nome">
          </div>
          <div class="form-group">
            <label for="editSobrenome">Sobrenome:</label>
            <input v-model="compradorEditado.sobrenome" id="editSobrenome" class="form-control" placeholder="Sobrenome">
          </div>
          <div class="form-group">
            <label for="editEmail">Email:</label>
            <input v-model="compradorEditado.email" id="editEmail" class="form-control" placeholder="Email">
          </div>
          <div class="form-group">
            <label for="editRA">RA:</label>
            <input v-model="compradorEditado.ra" id="editRA" class="form-control" placeholder="RA">
          </div>
          <div class="btn-salvar">
            <button type="submit" class="btn btn-primary">Salvar</button>
          </div>
        </form>
        <div v-if="loading">Salvando...</div>
        <div v-if="error" class="error-message">{{ error }}</div>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    props: {
      modalVisivel: Boolean,
      compradorEditado: Object,
      fecharModal: Function,
    },
    data() {
      return {
        loading: false,
        error: null,
      };
    },
    methods: {
      async salvarEdicao() {
        try {
          this.loading = true;
          this.error = null;
  
          console.log('Salvando edição...');
          const response = await axios.put('https://localhost:7127/api/Comprador', this.compradorEditado);
          alert("Comprador editado com sucesso!!");
          window.location.reload(true);
          console.log('Comprador atualizado:', response.data);
          this.$emit('edicaoConcluida', response.data);
  
          // Fechar o modal
          this.fecharModal();
        } catch (error) {
          console.error('Erro na atualização do comprador:', error);
          this.error = 'Erro ao salvar. Por favor, tente novamente.';
        } finally {
          this.loading = false;
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
  background-color: rgba(0, 0, 0, 0.4);
}

.modal-content {
  background-color: #fefefe;
  margin: 10% auto;
  padding: 20px;
  border: 1px solid #888;
  width: 50%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.close {
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
  cursor: pointer;
}

.close:hover,
.close:focus {
  color: black;
  text-decoration: none;
}

.form-group {
  margin-bottom: 15px;
}

.error-message {
  color: red;
  margin-top: 10px;
}

.btn-salvar{
    display: flex;
    justify-content: center;
}
</style>