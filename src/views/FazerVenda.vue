<template>
  <div id="ep-main">
    <div class="container">
      <p class="Login">Venda</p>
      <div class="row">
        <div class="col-md-6 margin-input">
          <label for="comprador">Comprador</label>
          <input maxlength="7" v-model="formData.Compradores" type="number" class="form-control inputs" id="comprador" placeholder="Comprador ID" />
        </div>
        <div class="col-md-6 margin-input">
          <label for="evento">Evento</label>
          <input maxlength="7" v-model="formData.Eventos" type="number" class="form-control inputs" id="evento" placeholder="Evento ID" />
        </div>
      </div>
      <div class="row">
        <div class="col-md-8 margin-input">
          <label for="dataEvento">Data do Evento</label>
          <input maxlength="8" v-model="formData.Data" type="date" class="form-control inputs" id="dataEvento" />
        </div>
        <div class="col-md-4 margin-input">
          <label for="QtdIngresso">Quantidade de Ingresso</label>
          <input maxlength="8" v-model="formData.QtdIngresso" type="number" min="1" class="form-control inputs" id="QtdIngresso" placeholder="Quantidade de ingresso" />
        </div>
      </div>
      <div class="cadEvento">
        <button type="button" class="buttonEvento" @click="concluirVenda">Concluir</button>
      </div>
    </div>
  </div>
</template>

<script>
import { Alert } from "bootstrap";
import "../components/style/style.css";
import axios from "axios";

export default {
  data() {
    return {
      formData: {
        Compradores: null,
        Eventos: null,
        Data: null,
        QtdIngresso: null,
      },
    };
  },
  methods: {
    concluirVenda() {
      if(this.formData.Compradores == null){
        alert('Por Favor, Informe o Id do Comprador');
        return;
      }
      if(this.formData.Eventos == null){
        alert('Por Favor, Informe o Id do Evento');
        return;
      }
      if(this.formData.Data == null){
        alert('Por Favor, Informe a Data do Evento');
        return;
      }
      if(this.formData.QtdIngresso == null){
        alert('Por Favor, Informe a quantiade de Ingresso');
        return;
      }
      axios.post('https://localhost:7127/api/Venda?idComprador=2&idEvento=2&qntdIng=100', this.formData).then((response) => {
        alert('Venda concluída com sucesso!!');
        this.limparCampos();
        return;
      })
      .catch((error) => {
        alert('Erro ao concluir a venda!!');
        console.error('Erro ao concluir a venda:', error);
      });
    },
    limparCampos(){
      this.formData.Compradores = null;
      this.formData.Eventos = null;
      this.formData.Data = null;
      this.formData.QtdIngresso = null;
    }
  },
};
</script>

<style scoped>
@import url('https://fonts.cdnfonts.com/css/lexend-deca');
.Login {
  display: flex;
  justify-content: center;
  color: black;
  text-transform: uppercase;
  font-size: 60px;
  font-family: "Lexend Deca", sans-serif;
} 

#ep-main {
  background-color: white;
  margin-top: 5em;
  font-family: "Lexend Deca", sans-serif;
}
label {
  color: white;
}
input {
  border: none;
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

input[type="date"]:hover::-webkit-calendar-picker-indicator { opacity:0.05; }
input[type="date"]:hover::-webkit-calendar-picker-indicator:hover { opacity:0.15; }
</style>
