<template>
    <li v-bind:class="{selected: project.id == idSelectedItem}">
      <span class="size" v-bind:class="{done: !project.active}">
        <label class="checkbox style-g">
          <input type="checkbox" v-bind:checked="project.active" disabled>
          <div class="checkbox__checkmark"></div>
          <div class="checkbox__body">Активный: </div>
        </label>
        <strong>{{project.key}}</strong>
        {{project.name}}
      </span>
      <span class="buttons">
        <button v-on:click="$emit('select-project', project)">&#10000;</button>
        <button v-on:click="$emit('remove-project', project.id)">x</button>
      </span>
    </li>
</template>

<script>
export default {
  props: ["project", "idSelectedItem"]
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

.size {
  white-space: nowrap;
  overflow: hidden;
  position: relative;
}

input {
  margin-right: 1rem;
}

button {
  margin-right: 3px;
  height: 25px;
  width: 30px;
}

.buttons {
  white-space: nowrap;
  margin-left: 3px;
}

.done {
  text-decoration: line-through;
}

strong {
  margin-left: 2rem;
}

</style>
