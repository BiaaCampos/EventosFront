<template>
  <div id="ep-main"></div>
    <div class="container">
      <p class="Login">Comprador</p>
      <div class="row">
        <div class="col-md-6 margin-input">
          <label for="nome">Nome</label>
          <input v-model="formData.nome" type="text" class="form-control inputs" id="nome" placeholder="Nome do comprador" />
        </div>
        <div class="col-md-6 margin-input">
          <label for="sobrenome">Sobrenome</label>
          <input v-model="formData.sobrenome" type="text" class="form-control inputs" id="sobrenome" placeholder="Sobrenome do comprador" />
        </div>
      </div>
      <div class="row">
        <div class="col-md-6 margin-input">
          <label for="email">Email</label>
          <input v-model="formData.email" type="email" class="form-control inputs" id="email" placeholder="user@user.com" />
        </div>
        <div class="col-md-2 margin-input">
          <label for="senha">Senha</label>
          <input v-model="formData.senha" type="password" class="form-control inputs" id="senha" placeholder="...." />
        </div>
        <div class="col-md-4 margin-input">
          <label for="ra">RA</label>
          <input v-model="formData.ra" type="number" class="form-control inputs" id="ra" placeholder="RA" />
        </div>
        <div class="col-md-4 margin-input">
          <label for="dataEvento">Data do Cadastro</label>
          <input v-model="formData.dataEvento" type="date" class="form-control inputs" id="dataEvento" />
        </div>
        <div class="col-md-4" id="ativo">
          <label class="switch">
            <input type="checkbox" @click="toggleCheckbox">
            <div class="slider round"></div>
          </label>
          <p style="padding: 12px 0 0 12px">{{ checkbox }}</p>
        </div>
      </div>
      <div class="cadEvento">
        <button type="button" class="buttonEvento" @click="cadastrarComprador">Cadastrar</button>
      </div>
      <!-- Alertas -->
      <div v-if="successMessage" class="alert alert-success top-alert" role="alert">
        {{ successMessage }}
      </div>
      <div v-if="errorMessage" class="alert alert-danger top-alert" role="alert">
        {{ errorMessage }}
      </div>
    </div>
</template>


<script>
import { ref } from 'vue';
import axios from 'axios';

export default {
  setup() {
    const formData = ref({
      nome: '',
      sobrenome: '',
      email: '',
      senha: '',
      ra: '', 
      dataEvento: '',
    });

    const checkbox = ref(false);
    const successMessage = ref('');
    const errorMessage = ref('');

    const toggleCheckbox = () => {
      checkbox.value = !checkbox.value;
    };

    const cadastrarComprador = () => {
      const dataToSend = {
        nome: formData.value.nome,
        sobrenome: formData.value.sobrenome,
        email: formData.value.email,
        senha: formData.value.senha, 
        ra: formData.value.ra, 
        dataEvento: formData.value.dataEvento,
        checkbox: checkbox.value,
      };

      axios
        .post('https://localhost:7127/api/Comprador', dataToSend)
        .then((response) => {
          console.log('Dados enviados com sucesso:', response.data);
          // Limpar os campos após o envio bem-sucedido
          formData.value.nome = '';
          formData.value.sobrenome = '';
          formData.value.email = '';
          formData.value.senha = '';
          formData.value.ra = '';
          formData.value.dataEvento = '';
          checkbox.value = true;
          // Exibir mensagem de sucesso
          successMessage.value = 'Comprador cadastrado com sucesso!';
          errorMessage.value = ''; // Limpar mensagem de erro
          // Esconder a mensagem após 3 segundos
          setTimeout(() => {
            successMessage.value = '';
          }, 3000);
        })
        .catch((error) => {
          console.error('Erro ao enviar dados para o servidor:', error);
          // Exibir mensagem de erro
          successMessage.value = '';
          errorMessage.value = 'Erro ao cadastrar comprador. Tente novamente.';
          // Esconder a mensagem de erro após 3 segundos
          setTimeout(() => {
            errorMessage.value = '';
          }, 3000);
        });
    };

    return {
      formData,
      checkbox,
      successMessage,
      errorMessage,
      toggleCheckbox,
      cadastrarComprador,
    };
  },
};
</script>










<style scoped>
@import url('https://fonts.cdnfonts.com/css/lexend-deca');
#ep-main {
  background-color: white;
  margin-top: 5em;
  font-family: "Lexend Deca", sans-serif;
}

.switch {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 60px;
  height: 34px;
}

.switch input {
  display: none;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

input:checked + .slider {
  background-color: #101010;
}

input:focus + .slider {
  box-shadow: 0 0 1px #101010;
}

input:checked + .slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}

.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}

#ativo {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 25px;
  color: white;
}
.Login {
  display: flex;
  justify-content: center;
  color: black !important;
  text-transform: uppercase;
  font-size: 60px;
  font-family: "Lexend Deca", sans-serif;
}
label {
  color: white;
}

.cadEvento {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 2em;
}

.buttonEvento {
  width: 250px;
  height: 50px;
  border-radius: 50px;
  border: 1px solid #699bf7;
  color: #699bf7;
  background: #fff;
  box-shadow: 0px 4px 20px 0px rgba(105, 155, 247, 0.5);
}
.width-cont {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}
.container {
  width: 925px;
  height: 650px;
  padding: 5em;
  border-radius: 20px;
  background: #FFF;
  box-shadow:0px 4px 20px 0px rgba(105, 155, 247, 0.5);
}


.margin-input {
  margin-top: 10px;
}

input[type="date"] {
  display:block;
  position:relative;
  font-size:1rem;
  font-family:monospace;  
  border:1px solid #8292a2;
  border-radius:0.25rem;
  background:
    white
    url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='20' height='22' viewBox='0 0 20 22'%3E%3Cg fill='none' fill-rule='evenodd' stroke='%23688EBB' stroke-linecap='round' stroke-linejoin='round' stroke-width='2' transform='translate(1 1)'%3E%3Crect width='18' height='18' y='2' rx='2'/%3E%3Cpath d='M13 0L13 4M5 0L5 4M0 8L18 8'/%3E%3C/g%3E%3C/svg%3E")
    right 1rem
    center
    no-repeat;
  
  cursor:pointer;
}
.inputs {
  border: 1px solid gray;

}
input[type="date"]:focus {
  outline: none;
}
::-webkit-datetime-edit {}
::-webkit-datetime-edit-fields-wrapper {}
::-webkit-datetime-edit-month-field:hover,
::-webkit-datetime-edit-day-field:hover,
::-webkit-datetime-edit-year-field:hover {
  background:rgba(0, 120, 250, 0.1);
}
::-webkit-datetime-edit-text {
  opacity:0;
}
::-webkit-clear-button,
::-webkit-inner-spin-button {
  display:none;
}
::-webkit-calendar-picker-indicator {
  position:absolute;
  width:2.5rem;
  height:100%;
  top:0;
  right:0;
  bottom:0;
  
  opacity:0;
  cursor:pointer;
  
  color:rgba(0, 120, 250, 1);
  background:rgba(0, 120, 250, 1);
 
}

.top-alert {
  position: fixed;
  top: 1em;
  left: 50%;
  transform: translateX(-50%);
  width: 100%;
  z-index: 1000;
  width: 30em;
}

input[type="date"]:hover::-webkit-calendar-picker-indicator { opacity:0.05; }
input[type="date"]:hover::-webkit-calendar-picker-indicator:hover { opacity:0.15; }
</style>