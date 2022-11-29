<template>
  <label class="checkbox style-g">
    <input type="checkbox" v-model="this.selectedTask.active">
    <div class="checkbox__checkmark"></div>
    <div class="checkbox__body">Активный: </div>
  </label>
  <select id="inputKey" v-model="this.selectedTask.key_project">
    <option v-for="project of this.availableProjects" v-bind:value="project.id">{{project.name}}</option>
  </select>
  <input id="inputName" type="text" v-model="this.selectedTask.name"  placeholder="Имя задачи">
  <button v-on:click="this.$emit('edit-task', this.selectedTask)">{{this.button_text}}</button>
</template>

<script>
export default {
  props: ["selectedTask"],
  data() {
    return {
      availableProjects: JSON.parse(localStorage.getItem("projects")),

      button_text: "Добавить"
    }
  },
  methods: {
    setButtonText() {
      if (this.selectedTask.id == 0) {
        this.button_text = "Добавить"
      } else {
        this.button_text = "Изменить"
      }
    }
  },
  beforeUpdate() {
    this.setButtonText()
  }
}

</script>

<style scoped>

#inputKey {
  width: 100px;
  margin-left: 2rem;
}

#inputName {
  width: 300px;
  margin-left: 1rem;
  margin-right: 1rem;
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