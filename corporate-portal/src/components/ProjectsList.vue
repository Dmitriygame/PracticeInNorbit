<template>
  <div>
    <ul>
      <ProjectItem
          v-for="project of projects"
          v-bind:project="project"
          v-on:remove-project="removeProject"
      />
    </ul>
  </div>
</template>

<script>
import ProjectItem from "@/components/ProjectItem";
export default {
  props: ["projects"],
  components: {
    ProjectItem
  },
  methods: {
    removeProject(id) {
      this.$emit("remove-project", id)
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
