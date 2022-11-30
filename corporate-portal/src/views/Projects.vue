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
import ProjectsList from "@/components/Projects/ProjectsList"
import EditProject from "@/components/Projects/EditProject"
export default {
  data() {
    return {
      projects: JSON.parse(localStorage.getItem("projects")),
      selectedProject: {
        id: null,
        key: "",
        name: null,
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
      if(changedProject.id == null) {
        const newProject = {
          id: Date.now(),
          key: changedProject.key,
          name: changedProject.name,
          active: changedProject.active
        }
        if (newProject.name == "" || newProject.name == null) {
          newProject.name = "Новый проект";
        }
        this.projects.push(newProject);
      }
      //edit
      else {
        for (let currentProject of this.projects) {
          if (changedProject.id == currentProject.id) {
            currentProject.key = changedProject.key;
            if (changedProject.name == "" || changedProject.name == null) {
              currentProject.name = "Пустой проект";
            } else {
              currentProject.name = changedProject.name;
            }
            currentProject.active = changedProject.active;
            break;
          }
        }
      }
      this.selectedProject.id = null;
      this.selectedProject.key = "";
      this.selectedProject.name = null;

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