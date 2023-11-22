<template>
  <div id="ep-main">
    <div class="container">
      <p class="Login">Cadastrar Evento</p>
      <div class="row">
        <div class="col-md-8 margin-input">
          <label for="NomeEvento">Nome do Evento</label>
          <input
            v-model="formDataEvento.NomeEvento"
            type="text"
            id="NomeEvento"
            class="form-control inputs"
            placeholder="Digite o nome do Evento..."
          />
        </div>
        <div class="col-md-4 margin-input">
          <label for="ValorIngresso">Valor do Ingresso</label>
          <input
            v-model="formDataEvento.ValorIngresso"
            type="number"
            min="1"
            class="form-control inputs"
            id="ValorIngresso"
            placeholder="Preço"
          />
        </div>
      </div>
      <div class="row">
        <div class="col-md-3 margin-input">
          <label for="DataEvento">Data do Evento</label>
          <input
            v-model="formDataEvento.DataEvento"
            type="date"
            class="form-control inputs"
            id="DataEvento"
          />
        </div>
        <div class="col-md-2 margin-input">
          <label for="QtdLimiteIngresso">Qtd Ingressos</label>
          <input
            v-model="formDataEvento.QtdLimiteIngresso"
            type="number"
            min="1"
            class="form-control inputs"
            id="QtdLimiteIngresso"
            placeholder="Qtd ingresso"
          />
        </div>
        <div class="col-md-5 margin-input">
          <label for="LocalEvento">Local do Evento</label>
          <input
            v-model="formDataEvento.LocalEvento"
            type="text"
            id="LocalEvento"
            class="form-control inputs"
            placeholder="Digite o local do evento..."
          />
        </div>
        <div class="col-md-2" id="ativo">
          <label class="switch">
            <input
              v-model="formDataEvento.Ativo"
              type="checkbox"
              @click="toggleCheckbox"
            />
            <div class="slider round"></div>
          </label>
          <p >{{ formDataEvento.Ativo }}</p>
        </div>
      </div>
      <div class="row">
        <div class="col-md-12 margin-input">
          <label for="Descricao">Descrição do Evento</label>
          <textarea
            placeholder="Escreva aqui a descrição do evento"
            v-model="formDataEvento.Descricao"
            class="form-control inputs"
          ></textarea>
        </div>
      </div>
      <div class="cadEvento">
        <button type="button" class="buttonEvento" @click="cadastrarEvento">
          Cadastrar
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import "../components/style/style.css";
import { ref, onMounted } from "vue";
import axios from "axios";

export default {
  setup() {
    const formDataEvento = ref({
      NomeEvento: "",
      LocalEvento: "",
      DataEvento: "",
      ValorIngresso: "",
      QtdLimiteIngresso: "",
      Ativo: false,
      Descricao: "",
    });

    const checkbox = ref(false);
    const evento = ref([]);

    const toggleCheckbox = () => {
      checkbox.value = !checkbox.value;
    };

    const cadastrarEvento = () => {
      const dataToSendEvent = {
        NomeEvento: formDataEvento.value.NomeEvento,
        LocalEvento: formDataEvento.value.LocalEvento,
        DataEvento: formDataEvento.value.DataEvento,
        ValorIngresso: formDataEvento.value.ValorIngresso,
        QtdLimiteIngresso: formDataEvento.value.QtdLimiteIngresso,
        Descricao: formDataEvento.value.Descricao,
        Ativo: formDataEvento.value.Ativo,
      };
      axios
        .post("https://localhost:7127/api/Evento", dataToSendEvent)
        .then((response) => {
          console.log("Dados enviados com sucesso:", response.data);
          // Limpar os campos após o envio bem-sucedido
          formDataEvento.value.NomeEvento = "";
          formDataEvento.value.LocalEvento = "";
          formDataEvento.value.DataEvento = "";
          formDataEvento.value.ValorIngresso = "";
          formDataEvento.value.QtdLimiteIngresso = "";
          formDataEvento.value.Descricao = "";
          checkbox.value = false;
        })
        .catch((error) => {
          console.error("Erro ao enviar dados para o servidor:", error);
        });
    };

    onMounted(async () => {
      try {
        const response = await axios.get("https://localhost:7127/api/Evento");
        evento.value = response.data.$values;
        console.log(evento.value);
      } catch (error) {
        console.error("Erro na solicitação:", error);
      }
    });

    return {
      formDataEvento,
      checkbox,
      evento,
      toggleCheckbox,
      cadastrarEvento,
    };
  },
};
</script>

<style scoped>
@import url("https://fonts.cdnfonts.com/css/lexend-deca");
#ep-main {
  background-color: white;
  margin-top: 5em;
  font-family: "Lexend Deca", sans-serif;
}

.form-control:focus {
    color: black;
    background-color: white;
    outline: 0;
    box-shadow: none;
}
.Login {
  display: flex;
  justify-content: center;
  color: black;
  text-transform: uppercase;
  font-size: 60px;
  font-family: "Lexend Deca", sans-serif;
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
  display: block;
  position: relative;
  font-size: 1rem;
  font-family: monospace;
  border: 1px solid #8292a2;
  border-radius: 0.25rem;
  background: white
    url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='20' height='22' viewBox='0 0 20 22'%3E%3Cg fill='none' fill-rule='evenodd' stroke='%23688EBB' stroke-linecap='round' stroke-linejoin='round' stroke-width='2' transform='translate(1 1)'%3E%3Crect width='18' height='18' y='2' rx='2'/%3E%3Cpath d='M13 0L13 4M5 0L5 4M0 8L18 8'/%3E%3C/g%3E%3C/svg%3E")
    right 1rem center no-repeat;
  cursor: pointer;
}

#NomeEvento  {
  border: 1px solid gray;
}

.inputs {
  border: 1px solid gray;

}
input[type="date"]:focus {
  outline: none;
}

::-webkit-datetime-edit {
}
::-webkit-datetime-edit-fields-wrapper {
}
::-webkit-datetime-edit-month-field:hover,
::-webkit-datetime-edit-day-field:hover,
::-webkit-datetime-edit-year-field:hover {
  background: rgba(0, 120, 250, 0.1);
}
::-webkit-datetime-edit-text {
  opacity: 0;
}
::-webkit-clear-button,
::-webkit-inner-spin-button {
  display: none;
}
::-webkit-calendar-picker-indicator {
  position: absolute;
  width: 2.5rem;
  height: 100%;
  top: 0;
  right: 0;
  bottom: 0;

  opacity: 0;
  cursor: pointer;

  color: rgba(0, 120, 250, 1);
  background: rgba(0, 120, 250, 1);
}

input[type="date"]:hover::-webkit-calendar-picker-indicator {
  opacity: 0.05;
}
input[type="date"]:hover::-webkit-calendar-picker-indicator:hover {
  opacity: 0.15;
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
label {
  color: white;
}
input {
  border: none;
}
</style>
