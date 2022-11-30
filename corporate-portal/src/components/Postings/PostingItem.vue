<template>
    <li v-bind:class="{selected: posting.id == idSelectedItem}">
      <span>
        {{posting.date}}
        <b id="posting_hours">{{posting.hours}}</b>
        <router-link id="link" to="/tasks">{{this.taskName}}</router-link>
        {{posting.name}}
      </span>
      <span>
        <button v-on:click="$emit('select-posting', posting)">&#10000;</button>
        <button v-on:click="$emit('remove-posting', posting.id)">x</button>
      </span>
    </li>
</template>

<script>

export default {
  props: ["posting", "idSelectedItem"],
  data() {
    return {
      tasks: JSON.parse(localStorage.getItem("tasks"))
    }
  },
  computed: {
    taskName: function () {
      for (let task of this.tasks) {
        if (task.id === this.posting.id_key_task) {
          return task.name;
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

#link, #posting_hours {
  margin-left: 1rem;
}

button {
  margin-right: 3px;
  height: 25px;
  width: 30px;
}

</style>
