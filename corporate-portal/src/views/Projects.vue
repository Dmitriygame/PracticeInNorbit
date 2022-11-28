<template>
  <div>
    <h2>Проекты</h2>
    <hr>
    <EditProject
        v-bind:selectedProject="this.selectedProject"

        @edit-project="editProject"
    />
    <hr>
    <ProjectsList
        v-bind:projects="projects"
        v-bind:idSelectedItem="this.selectedProject.id"

        @remove-project="removeProject"
        @select-project="selectProject"
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
      selectedProject: {
        id: 0,
        key: "",
        name: "",
        active: true
      }
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
    editProject(changedProject) {
      //add
      if(changedProject.id == 0) {
        const newProject = {
          id: Date.now(),
          key: changedProject.key,
          name: changedProject.name,
          active: changedProject.active
        }
        this.projects.push(newProject);
      }
      //edit
      else {
        for (let currentProject of this.projects) {
          if (changedProject.id == currentProject.id) {
            currentProject.key = changedProject.key;
            currentProject.name = changedProject.name;
            currentProject.active = changedProject.active;
            break;
          }
        }
      }
      this.selectedProject.id = 0;
      this.selectedProject.key = "";
      this.selectedProject.name = "";

      localStorage.setItem("projects", JSON.stringify(this.projects));
    },

    selectProject(project) {
      this.selectedProject.id = project.id;
      this.selectedProject.key = project.key;
      this.selectedProject.name = project.name;
      this.selectedProject.active = project.active;
    }
  }
}
</script>