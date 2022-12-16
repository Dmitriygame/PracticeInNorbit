<template>
    <li v-bind:class="{ selected: this.posting.id == this.idSelectedItem,
                        not_enough_time: this.posting.hours < 8,
                        normal_time: this.posting.hours == 8,
                        excess_time: this.posting.hours > 8}">
      <span class="size">
        {{posting.date}}
        <b id="posting_hours">{{posting.hours}}</b>
        <strong><router-link id="link" to="/tasks">{{this.taskName}}</router-link></strong>
        <span :title="this.posting.name">{{posting.name}}</span>
      </span>
      <span class="buttons">
        <button @click="$emit('select-posting', posting)">&#10000;</button>
        <button @click="$emit('remove-posting', posting.id)">&#10006;</button>
      </span>
    </li>
</template>

<script>

export default {
  props: ["posting", "tasks", "idSelectedItem"],

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

.not_enough_time {
  color: black;
  background-color: yellow;
}

.normal_time {
  color: black;
  background-color: green;
}

.excess_time {
  background-color: darkred;
}

.selected {
  background-color: aqua;
}

#posting_hours {
  margin-left: 1rem;
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

.size {
  white-space: nowrap; /* Отменяем перенос текста */
  overflow: hidden; /* Обрезаем содержимое */
  position: relative; /* Относительное позиционирование */
}

</style>
