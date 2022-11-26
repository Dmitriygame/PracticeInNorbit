<template>
    <li>
      <span v-bind:class="{done: !project.active}">
        <input type="checkbox" v-on:change="project.active = !project.active">
        <strong>{{project.key}}</strong>
        {{project.name}}
      </span>
      <span>
        <button>&#10000;</button>
        <button v-on:click="$emit('remove-project', project.id)">x</button>
      </span>
    </li>
</template>

<script>
export default {
  props: {
    project: {
      type: Object,
      required: true
    }
  }
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

input {
  margin-right: 1rem;
}

span {
  vertical-align: center;
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
