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
localStorage.clear()

if (localStorage.length == 0) {
  let array = [
    {id: 1, key: "CRM", name: "Проект №1", active: true},
    {id: 2, key: "CRM", name: "Проект №2", active: false},
    {id: 3, key: "DRM", name: "Проект №3", active: true},
  ]
  localStorage.setItem("projects", JSON.stringify(array));

      array = [
    {id: 1, key_project: 2, name: "Задача №1", active: true},
    {id: 2, key_project: 2, name: "Задача №2", active: false},
    {id: 3, key_project: 3, name: "Задача №3", active: true},
  ]
  localStorage.setItem("tasks", JSON.stringify(array));

      array = [
    {id: 1, date: "2022-12-01", hours: 8, id_key_task: 1, name: "Проводка №1"},
    {id: 2, date: "2022-12-02", hours: 5, id_key_task: 3, name: "Проводка №2"},
    {id: 3, date: "2022-12-02", hours: 12, id_key_task: 3, name: "Проводка №3"},
  ]
  localStorage.setItem("postings", JSON.stringify(array));
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
