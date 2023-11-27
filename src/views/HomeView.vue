<template>
  <main>
    <div class="container-fluid d-flex justify-content-center">
      <div class="containerHome">
        <div class="image1"><p class="p"></p></div>
        <div class="card bg-dark text-white image">
          <img src="../components/image/coding-bootcamp-site-geral.png" class="card-img image" alt="...">
        </div> 
      </div>
    </div>
    <div class="container-fluid d-flex justify-content-center">
      <div class="input-group mb-3 input-search">
        <input type="text" class="form-control input-text" placeholder="Pesquisar eventos" aria-label="Pesquisar eventos" aria-describedby="button-addon2">
        <button class="btn btn-outline-secondary" type="button" id="button-addon2">Pesquisar</button>
      </div>
    </div>
    <div class="container-fluid d-flex justify-content-center" v-for="x in eventos">
      <div class="container">
        <div class="row mt-4">
          <div class="col-sm-6 col-md-6 col-lg-3">
            <div class="card" style="width: 20rem;">
              <img src="https://oficial.unimar.br/wp-content/uploads/2022/10/BANNER_EVENTOS-5.jpg" class="card-img-top" alt="..." style="height: 8em;">
              <div class="card-body">
                <h5 class="card-title title-homePage">{{x.nomeEvento}}</h5>
                <p class="card-text"><b>Valor dos ingressos:</b> R$ {{x.valorIngresso}}</p>
                <p class="card-text"><b>Local do Evento:</b> {{x.localEvento}}</p>
                <br>
                <p class="card-text text-center"><b>Para se inscrever, clique no botão abaixo:</b></p>
                <div class="button-inscrever">
                  <a href="#" class="btn btn-primary button-homePage">Inscrever</a>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

  </main>
</template>

<script>
import "../components/style/style.css";
import axios from "axios";
import { ref, computed, onMounted, reactive } from 'vue';
// import axios from 'axios';

export default {
  data() {
    return {
      eventos: []
    };
  },
  methods: {
    getEventos(){
      // this.eventos = [{nome: 'TESTE'}, {nome: 'teste1'}];
      axios.get('https://localhost:7127/api/evento').then((res) => {
        console.log(res);
        this.eventos = res.data.$values
      })
    }
  },
  mounted: function () {
    this.getEventos();
  }
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

main {
  height: calc(100vh - 100px);
  background-image: url("../components/image/initialPage.png");
  background-repeat: no-repeat;
  background-position: right;
  background-size: cover;
  overflow-x: hidden;
}

.image{
  width: 83em;
  height: 15em;
  border-radius: 20px;
}

.p{
  padding: 20px;
}

.input-search{
  width: 50em;
  top: 15px;
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

.button-homePage:hover {
  transform: scaleX(1.1);
  background-color: #014b96;
}

.button-inscrever{
  display: flex;
  justify-content: center;
}

.title-homePage{
  text-transform: uppercase;
  display: flex;
  justify-content: center;
  margin-bottom: 0.5em;
  margin-top: 0.5em;
  color: #000235;
  text-decoration: overline;
}
</style>