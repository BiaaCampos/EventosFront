<!-- <template>
    <div class="app">
      <div class="container">
        <p class="Login">Editar Comprador</p>
        <div class="row">
          <div class="col-md-6 margin-input">
            <label for="nome">Nome</label>
            <input v-model="comprador.nome" type="text" class="form-control inputs" id="nome" placeholder="Nome do comprador" />
          </div>
          <div class="col-md-6 margin-input">
            <label for="sobrenome">Sobrenome</label>
            <input v-model="comprador.sobrenome" type="text" class="form-control inputs" id="sobrenome" placeholder="Sobrenome do comprador" />
          </div>
        </div>
        <div class="row">
          <div class="col-md-6 margin-input">
            <label for="email">Email</label>
            <input v-model="comprador.email" type="email" class="form-control inputs" id="email" placeholder="user@user.com" />
          </div>
          <div class="col-md-2 margin-input">
            <label for="senha">Senha</label>
            <input v-model="comprador.senha" type="password" class="form-control inputs" id="senha" placeholder="...." />
          </div>
          <div class="col-md-4 margin-input">
            <label for="ra">RA</label>
            <input v-model="comprador.ra" type="number" class="form-control inputs" id="ra" placeholder="RA" />
          </div>
        </div>
        <div class="row">
          <div class="col-md-4 margin-input">
            <label for="dataEvento">Data do Cadastro</label>
            <input v-model="comprador.dataEvento" type="date" class="form-control inputs" id="dataEvento" />
          </div>
          <!-- Adicione outros campos conforme necessário... -->
        </div>
        <div class="cadEvento">
          <button type="button" class="buttonEvento" @click="atualizarComprador">Atualizar</button>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import { ref, onMounted } from 'vue';
  import axios from 'axios';
  
  export default {
    setup() {
      const comprador = ref({
        id: null,
        nome: '',
        sobrenome: '',
        email: '',
        senha: '',
        ra: '',
        dataEvento: '',
      });
  
      const obterComprador = async () => {
        try {
          const id = parseInt(this.$route.params.id);
          const response = await axios.get(`https://localhost:7127/api/Comprador/${id}`);
          comprador.value = response.data;
        } catch (error) {
          console.error('Erro ao obter comprador:', error);
        }
      };
  
      const atualizarComprador = async () => {
        try {
          const id = parseInt(this.$route.params.id);
          await axios.put(`https://localhost:7127/api/Comprador/${id}`, comprador.value);
          console.log('Comprador atualizado com sucesso.');
          this.$router.push({ name: 'vizualizarCompradores' });
        } catch (error) {
          console.error('Erro ao atualizar comprador:', error);
        }
      };
  
      onMounted(async () => {
        await obterComprador();
      });
  
      return {
        comprador,
        atualizarComprador,
      };
    },
  };
  </script> -->
  
  <style scoped>
  /* Adicione estilos específicos do componente aqui, se necessário */
  </style>
  