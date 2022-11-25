<template>
  <input type="text" v-model="name">
  <button v-on:click="this.$emit('add-project', this.name),
          this.name = '' "
  >Добавить</button>
</template>

<script>
export default {
  data() {
    return {
      name: ""
    }
  }
}
</script>

<style scoped>
  input {
    width: 300px;
  }
</style>