<template>
  <div>
    <ul>
      <PostingItem
          v-for="posting of postings"
          v-bind:posting="posting"
          v-bind:idSelectedItem="idSelectedItem"
          v-on:remove-posting="removePosting"
          v-on:select-posting="selectPosting"
      />
    </ul>
  </div>
</template>

<script>
import PostingItem from "@/components/Postings/PostingItem";
export default {
  props: ["postings", "idSelectedItem"],
  components: {
    PostingItem
  },
  methods: {
    removePosting(id) {
      this.$emit("remove-posting", id);
    },
    selectPosting(posting) {
      this.$emit("select-posting", posting);
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
