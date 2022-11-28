<template>
  <div>
    <ul>
      <ProjectItem
          v-for="project of projects"
          v-bind:project="project"
          v-bind:idSelectedItem="idSelectedItem"
          v-on:remove-project="removeProject"
          v-on:select-project="selectProject"
      />
    </ul>
  </div>
</template>

<script>
import ProjectItem from "@/components/ProjectItem";
export default {
  props: ["projects", "idSelectedItem"],
  components: {
    ProjectItem
  },
  methods: {
    removeProject(id) {
      this.$emit("remove-project", id);
    },
    selectProject(project) {
      this.$emit("select-project", project);
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
