<template>
    <li v-bind:class="{selected: task.id == idSelectedItem}">
      <span v-bind:class="{done: !task.active}">
        <label class="checkbox style-g">
          <input type="checkbox" v-bind:checked="task.active" disabled>
          <div class="checkbox__checkmark"></div>
          <div class="checkbox__body">Активный: </div>
        </label>
        <router-link id="link" to="/projects">{{this.projectName}}</router-link>
        {{task.name}}
      </span>
      <span>
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

.selected {
  background-color: aqua;
}

input {
  margin-right: 1rem;
}

span {
  vertical-align: center;
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

.checkbox.style-g {
  display: inline-block;
  position: relative;
  padding-right: 40px;
  cursor: pointer;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.checkbox.style-g input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}
.checkbox.style-g input:checked ~ .checkbox__checkmark {
  background-color: #fff;
}
.checkbox.style-g input:checked ~ .checkbox__checkmark:after {
  opacity: 1;
  left: 8px;
}

.checkbox.style-g:hover input ~ .checkbox__checkmark {
  background-color: #eee;
}
.checkbox.style-g:hover input:checked ~ .checkbox__checkmark {
  background-color: #eee;
}
.checkbox.style-g .checkbox__checkmark {
  position: absolute;
  top: 1px;
  right: 0;
  height: 22px;
  width: 22px;
  background-color: #eee;
  transition: background-color 0.25s ease;
  border-radius: 4px;
}
.checkbox.style-g .checkbox__checkmark:after {
  content: "";
  position: absolute;
  left: -20px;
  top: -8px;
  width: 15px;
  height: 25px;
  border: solid #000;
  border-width: 0 4px 4px 0;
  transform: rotate(45deg);
  opacity: 0;
  transition: opacity 0.25s ease, left 0.25s ease;
}
.checkbox.style-g .checkbox__body {
  color: #333;
  line-height: 1.4;
  font-size: 16px;
  transition: font-weight 0.25s ease;
}

</style>
