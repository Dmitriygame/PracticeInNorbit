<template>
  <div>
    <ul>
      <ProjectItem
          v-for="project of projects"
          v-bind:project="project"
          v-bind:idSelectedItem="idSelectedItem"
          v-on:remove-project="removeProject"
          v-on:select-project-id="selectProjectId"
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
    selectProjectId(id) {
      this.$emit("select-project-id", id);
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
