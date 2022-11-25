<template>
    <li>
      <span v-bind:class="{done: !project.active}">
        <input type="checkbox"
               v-on:change="project.active = !project.active">
        <strong>{{project.id}}</strong>
        {{project.name}}
      </span>
      <button v-on:click="$emit('remove-project', project.id)">&times;</button>

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

.done {
  text-decoration: line-through;
}
</style>