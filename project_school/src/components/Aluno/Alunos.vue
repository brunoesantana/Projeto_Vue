<template>
  <div>
    <titulo :texto=" professorid != undefined ? 'Professor: ' + professor.nome : 'Todos os alunos'"/>
    <input type="text" placeholder="Nome do aluno" v-model="nome" v-on:keyup.enter="addAluno()">
    <button class="btn btn-input" @click="addAluno()">Adicionar</button>

    <table>
      <thead>
        <th class="col-pequeno">Matrícula</th>
        <th>Nome</th>
        <th class="col-pequeno"> Opções</th>
      </thead>
      <tbody v-if="alunos.length">
        <tr v-for="(aluno, index) in alunos" :key="index">
          <td class="centralizar-texto">{{aluno.id}}</td>
            <router-link tag="td" :to="`/alunodetalhe/${aluno.id}`" style="cursor: pointer;">
              {{aluno.nome}} {{aluno.sobrenome}}
            </router-link>
          <td class="centralizar-texto">
            <button class="btn btn-danger" @click="remover(aluno)">Remover</button>
          </td>
        </tr>
      </tbody>
      <tfoot v-else>Nenhum aluno encontrado</tfoot>
    </table>
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
      professorid: this.$route.params.prof_id,
      professor:{},
      nome: "",
      alunos: []
    };
  },
  created() {
    if (this.professorid) {
      this.CarregaProfessores();
      this.$http
        .get("http://localhost:3000/alunos?professor.id=" + this.professorid)
        .then(response => response.json())
        .then(alunos => (this.alunos = alunos));
    } else {
      this.$http
        .get("http://localhost:3000/alunos")
        .then(response => response.json())
        .then(alunos => (this.alunos = alunos));
    }
  },
  props: {},
  methods: {
    addAluno() {
      let _aluno = {
        nome: this.nome,
        sobrenome: "",
        professor:{
          id: this.professor.id,
          nome: this.professor.nome
        }
      };

      this.$http
        .post("http://localhost:3000/alunos", _aluno)
        .then(response => response.json())
        .then(alunoRetornado => {
          this.alunos.push(alunoRetornado);
          this.nome = "";
        });
    },
    remover(aluno) {
      this.$http.delete(`http://localhost:3000/alunos/${aluno.id}`).then(() => {
        let indice = this.alunos.indexOf(aluno);
        this.alunos.splice(indice, 1);
      });
    },
      CarregaProfessores(){
      this.$http
      .get("http://localhost:3000/professores/" + this.professorid)
      .then(response => response.json())
      .then(professor => {
        this.professor = professor;
      });
    }
  }
};
</script>

<style scoped>
input {
  width: calc(100% - 130px);
  padding-left: 5px;
  height: 20px;
}

.btn-input {
  width: 100px;
  background-color: blueviolet;
  border: 1px solid blueviolet;
  margin: 0px 0px 15px 20px;
}

.btn-input:hover {
  background-color: #fff;
  border: 1px solid blueviolet;
  transition: 0.3s;
  color: blueviolet;
}
</style>
