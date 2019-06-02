<template>
  <div>
    <titulo :texto="`Aluno: ${aluno.nome + ' ' + aluno.sobrenome }`" :btnVoltar="!visualizando">
      <button v-show="visualizando" class="btn btn-editar" @click="editar()">Editar</button>
    </titulo>

    <table>
      <tbody>
        <tr>
          <td class="coluna-header">Matrícula:</td>
          <td>
            <label>{{aluno.id}}</label>
          </td>
        </tr>
        <tr>
          <td class="coluna-header">Nome:</td>
          <td>
            <label v-if="visualizando">{{aluno.nome}}</label>
            <input v-else v-model="aluno.nome" type="text">
          </td>
        </tr>
        <tr>
          <td class="coluna-header">Sobrenome:</td>
          <td>
            <label v-if="visualizando">{{aluno.sobrenome}}</label>
            <input v-else v-model="aluno.sobrenome" type="text">
          </td>
        </tr>
        <tr>
          <td class="coluna-header">Data Nascimento:</td>
          <td>
            <label v-if="visualizando">{{aluno.dataNasc}}</label>
            <input v-else v-model="aluno.dataNasc" type="text">
          </td>
        </tr>
        <tr>
          <td class="coluna-header">Professor:</td>
          <td>
            <label v-if="visualizando">{{aluno.professor.nome}}</label>
            <select v-else v-model="aluno.professor">
              <option
                v-for="(professor, index) in professores"
                :key="index"
                v-bind:value="professor"
              >{{professor.nome}}</option>
            </select>
          </td>
        </tr>
      </tbody>
    </table>
    <div style="margin-top: 10px;">
      <div v-if="!visualizando">
        <button class="btn btn-salvar" @click="salvar(aluno)">Salvar</button>
        <button class="btn btn-cancelar" @click="cancelar()">Cancelar</button>
      </div>
    </div>
  </div>
</template>

<script>
import Titulo from "../_share/Titulo";
export default {
  components: {
    Titulo
  },
  data() {
    return {
      professores: [],
      aluno: {},
      idAluno: this.$route.params.id,
      visualizando: true
    };
  },
  created() {
    this.$http
      .get("http://localhost:3000/alunos/" + this.idAluno)
      .then(response => response.json())
      .then(aluno => (this.aluno = aluno));

    this.$http
      .get("http://localhost:3000/professores")
      .then(response => response.json())
      .then(professor => (this.professores = professor));
  },
  methods: {
    editar() {
      this.visualizando = !this.visualizando;
    },
    salvar(_aluno) {
      let _alunoEditar = {
        id: _aluno.id,
        nome: _aluno.nome,
        sobrenome: _aluno.sobrenome,
        dataNasc: _aluno.dataNasc,
        professor: _aluno.professor
      };

      this.$http.put(
        `http://localhost:3000/alunos/${_alunoEditar.id}`,
        _alunoEditar
      );

      this.visualizando = !this.visualizando;
    },
    cancelar() {
      this.visualizando = !this.visualizando;
    }
  }
};
</script>

<style scoped>
.coluna-header {
  width: 25%;
  background-color: blueviolet;
  font-weight: bold;
  color: white;
}

input,
select {
  background-color: transparent;
  border-bottom: 1px solid blueviolet !important;
}

input,
select {
  margin: 0;
  padding: 0px 10px;
  font-family: Montserrat;
  border: none;
  font-size: 1.2em;
  width: 95%;
  height: 100%;
  outline: none;
}

.btn-editar {
  width: 90px;
  float: right;
  background-color: darkslategrey;
  color: white;
  border: 2px solid darkslategrey;
}

.btn-editar:hover {
  background-color: white;
  color: darkslategrey;
  border: 2px solid darkslategrey;
}

label {
  margin: 0;
  padding: 5px 10px;
  font-family: Montserrat;
  border: none;
  font-size: 0.9em;
  width: 95%;
  height: 100%;
}

.btn-salvar {
  float: right;
  background-color: darkblue;
  color: white;
  border: 2px solid darkblue;
  margin-left: 20px;
}

.btn-salvar:hover {
  background-color: white;
  color: darkblue;
  border: 2px solid darkblue;
}

.btn-cancelar {
  float: right;
  background-color: darkorange;
  color: white;
  border: 2px solid darkorange;
}

.btn-cancelar:hover {
  background-color: white;
  color: darkorange;
  border: 2px solid darkorange;
}
</style>