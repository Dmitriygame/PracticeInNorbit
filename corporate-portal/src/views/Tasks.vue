<template>
  <div>
    <h2>Задачи</h2>
    <hr>
    <EditTask
        :selectedTask="this.selectedTask"
        :projects="this.projects"

        @edit-task="editTask"
    />
    <hr>
    <TasksList
        :tasks="tasks"
        :projects="projects"
        :idSelectedItem="this.selectedTask.id"

        @remove-task="removeTask"
        @select-task="selectTask"
    />
  </div>
</template>

<script>
import TasksList from "@/components/Tasks/TasksList"
import EditTask from "@/components/Tasks/EditTask"
export default {
  data() {
    return {
      tasks: JSON.parse(localStorage.getItem("tasks")),
      projects: JSON.parse(localStorage.getItem("projects")),
      selectedTask: {
        id: null,
        key_project: null,
        name: null,
        active: true
      }
    }
  },
  components: {
    TasksList, EditTask
  },
  methods: {
    removeTask(id) {
      this.tasks = this.tasks.filter(p => p.id != id);
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
    editTask(changedTask) {
      //add
      if(changedTask.id == null) {
        const newTask = {
          id: Date.now(),
          key_project: changedTask.key_project,
          name: changedTask.name,
          active: changedTask.active
        };
        if (newTask.name == "" || newTask.name == null) {
          newTask.name = "Новая задача";
        }
        this.tasks.push(newTask);
      }
      //edit
      else {
        for (let currentTask of this.tasks) {
          if (changedTask.id == currentTask.id) {
            currentTask.key_project = changedTask.key_project;
            if (changedTask.name == "" || changedTask.name == null) {
              currentTask.name = "Пустая задача";
            }
            else {
              currentTask.name = changedTask.name;
            }
            currentTask.active = changedTask.active;
            break;
          }
        }
      }
      this.selectedTask.id = null;
      this.selectedTask.key_project = null;
      this.selectedTask.name = null;

      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },

    selectTask(task) {
      this.selectedTask.id = task.id;
      this.selectedTask.key_project = task.key_project;
      this.selectedTask.name = task.name;
      this.selectedTask.active = task.active;
    }
  }
}
</script>