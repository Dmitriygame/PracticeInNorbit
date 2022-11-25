<template>
  <div>
    <h2>Проекты</h2>
    <hr>
    <AddProject
        @add-project="addProject"
    />
    <hr>
    <ProjectsList
        v-bind:projects="projects"
        @remove-project="removeProject"
    />
  </div>
</template>

<script>
import ProjectsList from "@/components/ProjectsList"
import AddProject from "@/components/AddProject"
export default {
  //name: 'App',
  data() {
    return {
      projects: [
        {id: 1, name: "Проект №1", active: true},
        {id: 2, name: "Проект №2", active: true},
        {id: 3, name: "Проект №3", active: true},
      ]
    }
  },
  components: {
    ProjectsList, AddProject
  },
  methods: {
    removeProject(id) {
      this.projects = this.projects.filter(p => p.id != id)
      console.log("remove")
    },
    addProject(name) {
      const newProject = {
        id: Date.now(),
        name: name,
        active: true
      }
      this.projects.push(newProject)
    }
  }
}
</script>