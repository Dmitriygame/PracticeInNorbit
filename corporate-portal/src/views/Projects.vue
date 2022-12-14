<template>
  <div>
    <h2>Проекты</h2>
    <hr>
    <EditProject
        :selectedProject="this.selectedProject"

        @edit-project="editProject"
    />
    <hr>
    <ProjectsList
        :projects="projects"
        :idSelectedItem="this.selectedProject.id"

        @remove-project="removeProject"
        @select-project="selectProject"
    />
  </div>
</template>

<script>
import ProjectsList from "@/components/Projects/ProjectsList"
import EditProject from "@/components/Projects/EditProject"

import { db } from "@/main"
import { collection, doc, getDocs, setDoc, deleteDoc } from 'firebase/firestore'

export default {
  data() {
    return {
      projects: [],

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

  beforeMount() {
    this.getProjects();
  },

  methods: {
    async getProjects() {
      this.projects = [];
      try {
        const querySnapshot = await getDocs(collection(db, "projects"));
        querySnapshot.forEach((doc) => {
          let project = doc.data();
          project.id = doc.id;
          this.projects.push(project);
        });
      }
      catch (e) {
        alert(`Возникла ошибка!\n${e}`);
      }
    },

    async removeProject(id) {
      this.projects = this.projects.filter(p => p.id != id);
      try {
        await deleteDoc(doc(db, "projects", id));
      }
      catch (e) {
        alert(`Возникла ошибка на стороне сервера!\n${e}`);
      }
    },

    async editProject(changedProject) {

      if (changedProject.name == "" || changedProject.name == null) {
        changedProject.name = "Пустой проект";
      }

      if (changedProject.id == null) {
        changedProject.id = Date.now();
      }

      try {
        await setDoc(doc(db, "projects", String(changedProject.id) ), {
          key: changedProject.key,
          name: changedProject.name,
          active: changedProject.active
        });
      }
      catch (e) {
        alert(`Возникла ошибка!\n${e}`);
      }

      this.getProjects();

      this.selectedProject.id = null;
      this.selectedProject.key = "";
      this.selectedProject.name = null;

    },

    selectProject(project) {
      this.selectedProject.id = project.id;
      this.selectedProject.key = project.key;
      this.selectedProject.name = project.name;
      this.selectedProject.active = project.active;
    },
  }
}

</script>