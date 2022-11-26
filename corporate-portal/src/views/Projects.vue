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
  data() {
    return {
      projects: JSON.parse(localStorage.getItem("projects")),
    }
  },
  components: {
    ProjectsList, AddProject
  },
  methods: {
    removeProject(id) {
      this.projects = this.projects.filter(p => p.id != id);
      localStorage.setItem("projects", JSON.stringify(this.projects));
    },
    addProject(name, key) {
      const newProject = {
        id: Date.now(),
        key: key,
        name: name,
        active: true
      }
      this.projects.push(newProject);
      localStorage.setItem("projects", JSON.stringify(this.projects));
    }
  }
}
</script>