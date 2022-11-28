<template>
  <div id="app">
    <h1>Портал учета рабочего времени</h1>
    <hr>
    <p><router-link to="/">Домой</router-link></p>
    <hr>

    <router-view  />

  </div>
</template>

<script>
  //localStorage.clear();

if (localStorage.length == 0) {
  let array = [
    {id: 0, key: "CRM", name: "Проект №1", active: true},
    {id: 2, key: "CRM", name: "Проект №2", active: false},
    {id: 3, key: "DRM", name: "Проект №3", active: true},
  ]
  localStorage.setItem("projects", JSON.stringify(array));
  localStorage.setItem("tasks", "");
  localStorage.setItem("postings", "");
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
