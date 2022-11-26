<template>
  <input type="text" v-model="key" placeholder="Код">
  <input id="inputName" type="text" v-model="name"  placeholder="Имя проекта">
  <button v-on:click="this.$emit('add-project', this.name, this.key),
          this.key='', this.name = '' "
  >Добавить</button>
</template>

<script>
export default {
  data() {
    return {
      key: "",
      name: ""
    }
  }
}
</script>

<style scoped>
  #inputName {
    width: 300px;
  }
</style>