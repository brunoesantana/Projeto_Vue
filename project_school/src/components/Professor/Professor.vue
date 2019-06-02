<template>
  <div>
    <titulo texto="Professores"/>
    <table>
      <thead>
        <th class="col-pequeno">Código</th>
        <th>Nome</th>
        <th class="col-pequeno">Alunos</th>
      </thead>
      <tbody v-if="professores.length">
        <tr v-for="(professor, index) in professores" :key="index">
          <td class="centralizar-texto"> {{professor.id}} </td>
          <router-link 
          :to="`/alunos/${professor.id}`" 
          tag="td" 
          style="cursor: pointer;">
            {{professor.nome}} {{professor.sobrenome}}
          </router-link>
          <td class="centralizar-texto"> {{professor.quantidadeAlunos}} </td>
        </tr>
      </tbody>
      <tfoot v-else> Nenhum professor encontrado </tfoot>
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
      professores: [],
      alunos: []
    };
  },
    created() {
    this.$http
      .get("http://localhost:3000/alunos")
      .then(response => response.json())
      .then(alunos => {
        this.alunos = alunos;
        this.CarregaProfessores();
      });
  },
  props: {},
  methods: {
    CarregaProfessores(){
      this.$http
      .get("http://localhost:3000/professores")
      .then(response => response.json())
      .then(professores => {
        this.professores = professores;
        this.RetornaQuantidadeDeAlunosPorProfessor();
      });
    },
    RetornaQuantidadeDeAlunosPorProfessor(){
      this.professores.forEach((professor, index) => {
        professor = {
          id: professor.id,
          nome: professor.nome,
          quantidadeAlunos: this.alunos.filter(aluno => aluno.professor.id == professor.id).length
        }
        this.professores[index] = professor;
      });
    }
  },
};
</script>

<style scoped>
</style>