<template>
  <div>
    <ul>
      <TaskItem
          v-for="task of tasks"
          v-bind:task="task"
          v-bind:idSelectedItem="idSelectedItem"
          v-on:remove-task="removeTask"
          v-on:select-task="selectTask"
      />
    </ul>
  </div>
</template>

<script>
import TaskItem from "@/components/Tasks/TaskItem";
export default {
  props: ["tasks", "idSelectedItem"],
  components: {
    TaskItem
  },
  methods: {
    removeTask(id) {
      this.$emit("remove-task", id);
    },
    selectTask(task) {
      this.$emit("select-task", task);
    }
  }
}
</script>

<style scoped>
  ul {
    list-style: none;
    margin: 0;
    padding: 0;
  }
</style>
