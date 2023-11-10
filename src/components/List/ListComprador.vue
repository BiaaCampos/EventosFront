<!-- <script setup>
import { ref, computed, onMounted, reactive } from 'vue';
import axios from 'axios';

const comprador = ref([]);

onMounted(async () => {
  try {
    const response = await axios.get('https://localhost:7127/api/comprador');
    comprador.value = response.data.$values;
    console.log(comprador.value);
  } catch (error) {
    console.error('Erro na solicitação:', error);
  }
});


</script>

  

  <script setup>
  import { ref, onMounted, watchEffect } from 'vue';
  import axios from 'axios';
  
  const evento = ref([]);
  
  onMounted(async () => {
    await carregarCompradores();
  });
  
  const carregarCompradores = async () => {
    const response = await axios.get('https://localhost:7127/api/evento');
    evento.value = response.data.$values;
  };
  
  watchEffect(() => {
    const cadastrarCompradorComponent = ref(null);
  
    cadastrarCompradorComponent.value && cadastrarCompradorComponent.value();
  });
  
  </script>
  
  <template>
    <main>
      <div class="container-fluid d-flex justify-content-center">
        <div class="input-group mb-3 input-search">
          <input type="text" class="form-control input-text" placeholder="Pesquisar Compradores" aria-label="Pesquisar eventos" aria-describedby="button-addon2">
          <button class="btn btn-outline-secondary" type="button" id="button-addon2">Pesquisar</button>
        </div>
      </div>
      <div class="centralizar">
        <div class="container bloco-anterior">
        </div>
      </div> 
      <CadastrarComprador @onCadastroSucesso="cadastrarCompradorComponent = $event" />  
    </main>
  </template> -->
  



<style scoped>
@import url('https://fonts.cdnfonts.com/css/lexend-deca');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family:'Lexend Deca', sans-serif;
}

.input-search{
  width: 50em;
  top: 30px;
  opacity: 0.9;
}

.input-text{
  padding: 6px;
}

.button-homePage{
  display: flex;
  justify-content: center;
  padding: 8px;
  background-color: #000235;
  margin-top: 1em;
  transition: transform 0.3s ease-in-out;
  width: 12em;
}

.bloco-anterior{
    background-color: #dfe9f77e;
    width: 100%;
    height: 45em;
    border-radius: 25px;
    display: flex;
    justify-content: center;
}

.centralizar {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 80vh;
  margin-top: 1em;
}

.list-comprador{
    margin-top: 1em;
    width: 98%;
}

.list-list{
    border-radius: 15px;
}

.test{
    background-color: transparent;
    padding: 5px 0px;
}

</style>
