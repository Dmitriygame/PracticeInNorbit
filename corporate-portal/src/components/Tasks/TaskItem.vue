<template>
    <li v-bind:class="{selected: task.id == idSelectedItem}">
      <span class="size" v-bind:class="{done: !task.active}">
        <label class="checkbox style-g">
          <input type="checkbox" v-bind:checked="task.active" disabled>
          <div class="checkbox__checkmark"></div>
          <div class="checkbox__body">Активный: </div>
        </label>
        <strong><router-link id="link" to="/projects">{{this.projectName}}</router-link></strong>
        {{task.name}}
      </span>
      <span class="buttons">
        <button v-on:click="$emit('select-task', task)">&#10000;</button>
        <button v-on:click="$emit('remove-task', task.id)">x</button>
      </span>
    </li>
</template>

<script>
export default {
  props: ["task", "idSelectedItem"],
  data() {
    return {
      projects: JSON.parse(localStorage.getItem("projects"))
    }
  },
  computed: {
    projectName: function () {
      for (let project of this.projects) {
        if (project.id === this.task.key_project) {
          return project.name;
        }
      }
    }
  },
}
</script>

<style scoped>
li {
  border: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  padding: .5rem 2rem;
  margin-bottom: 1rem;
}

.size {
  white-space: nowrap; /* Отменяем перенос текста */
  overflow: hidden; /* Обрезаем содержимое */
  position: relative; /* Относительное позиционирование */
}

#link {
  color: darkorchid;
}

.buttons {
  white-space: nowrap;
  margin-left: 3px;
}

.selected {
  background-color: aqua;
}

input {
  margin-right: 1rem;
}

#link {
  margin-left: 2rem;
}

button {
  margin-right: 3px;
  height: 25px;
  width: 30px;
}

.done {
  text-decoration: line-through;
}

</style>
