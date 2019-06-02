<template>
  <div class="barra-topo">
    <nav class="margem-principal">
        <router-link to="/professores">Professores</router-link>
        <router-link to="/todosalunos">Alunos</router-link>
        <router-link to="/sobre">Sobre</router-link>
    </nav>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.barra-topo{
    background-color: rgb(230, 230, 230);
}

nav{
    padding: 20px 20px 20px 0px;
}

nav a{
    padding: 10px;
    text-decoration: none;
    background-color: #fff;
    color: blueviolet;
    margin-right: 15px;
    transition: 0.3s;
}

nav a:hover{
  background-color: blueviolet;
  color: white;
  transition: 0.3s;
}

.margem-principal{
  width: 50%;
  margin: auto;
}

nav .router-link-active{
  background-color: blueviolet;
  color: white;
  transition: 0.3s;
}

</style>