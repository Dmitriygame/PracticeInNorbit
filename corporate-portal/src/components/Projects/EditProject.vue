<template>
  <label class="checkbox style-g">
    <input type="checkbox" v-model="this.selectedProject.active">
    <div class="checkbox__checkmark"></div>
    <div class="checkbox__body">Активный: </div>
  </label>
  <input id="inputKey" type="text" v-model="this.selectedProject.key" placeholder="Код">
  <input id="inputName" type="text" v-model="this.selectedProject.name"  placeholder="Имя проекта">
  <button v-on:click="this.$emit('edit-project', this.selectedProject)">{{this.button_text}}</button>
</template>

<script>
export default {
  props: ["selectedProject"],
  data() {
    return {
      key: this.selectedProject.key,
      name: this.selectedProject.name,
      active: this.selectedProject.active,
      button_text: "Добавить"
    }
  },
  methods: {
    setButtonText() {
      if (this.selectedProject.id == null) {
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