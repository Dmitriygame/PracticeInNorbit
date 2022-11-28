<template>
  <div>
    <h2>Проекты</h2>
    <hr>
    <EditProject
        @edit-project="editProject"
        v-bind:idSelectedItem="this.idSelectedItem"
    />
    <!--  -->

    <hr>
    <ProjectsList
        v-bind:projects="projects"
        v-bind:idSelectedItem="idSelectedItem"
        @remove-project="removeProject"
        @select-project-id="selectProjectId"
    />
  </div>
</template>

<script>
import ProjectsList from "@/components/ProjectsList"
import EditProject from "@/components/EditProject"
export default {
  data() {
    return {
      projects: JSON.parse(localStorage.getItem("projects")),
      idSelectedItem: 0
    }
  },
  components: {
    ProjectsList, EditProject
  },
  methods: {
    removeProject(id) {
      this.projects = this.projects.filter(p => p.id != id);
      localStorage.setItem("projects", JSON.stringify(this.projects));
    },
    editProject(name, key, active) {
      const newProject = {
        id: Date.now(),
        key: key,
        name: name,
        active: active
      }
      this.projects.push(newProject);
      localStorage.setItem("projects", JSON.stringify(this.projects));
    },
    selectProjectId(id) {
      this.idSelectedItem = id;
    }
  }
}
</script>