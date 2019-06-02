<template>
  <div id="app">
    <Nav></Nav>
    <div class="margem-principal">
      <router-view :key="$route.fullPath"></router-view>
    </div>
  </div>
</template>

<script>
import Alunos from "./components/Aluno/Alunos";
import Professor from "./components/Professor/Professor";
import Sobre from "./components/Sobre/Sobre";
import Nav from "./components/_nav/Nav";

export default {
  name: "app",
  components: {
    Alunos,
    Professor,
    Sobre,
    Nav
  }
};
</script>

<style>
@import url("http://fonts.googleapis.com/css?family=Montserrat:400,700");

body {
  background-color: #eee;
  font-family: "Montserrat";
  display: grid;
  justify-items: center;
}

body,
html {
  margin: 0;
  height: 100%;
}

#app {
  width: 100%;
}

.margem-principal {
  width: 50%;
  margin: auto;
}

.btn-danger {
  background-color: #fa4430;
  border: 1px solid #fa4430;
}

.btn {
  padding: 10px 15px;
  cursor: pointer;
  color: white;
  font-weight: bold;
  transition: 0.3s;
  border: 1px solid transparent;
  outline: none;
}

.btn:hover {
  background-color: white;
  border: 1px solid #fa4430;
  color: #fa4430;
  transition: 0.3s;
}

table {
  margin: 0;
  padding: 0;
  list-style-type: none;
  width: 100%;
}

table tr td {
  padding: 15px;
  font-size: 1.2em;
  color: #3e5252;
}

table tr {
  height: 60px;
}

table thead th {
  background-color: rgb(184, 208, 216) !important;
  font-size: 1.1em;
  padding: 10px 5px;
  text-align: center !important;
}

.centralizar-texto {
  text-align: center;
}

.col-pequeno {
  width: 15%;
}
</style>
