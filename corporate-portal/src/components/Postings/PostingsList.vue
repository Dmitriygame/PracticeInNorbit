<template>
  <div>
    <ul>
      <PostingItem
          v-for="posting of this.postingFiltered"
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
  props: ["postings", "idSelectedItem", "filterDate"],
  components: {
    PostingItem
  },

  computed: {
    postingFiltered: function () {
      if (this.filterDate == "all") {
        return this.postings;
      }
      else if (this.filterDate == "month") {
        let array = [];
        let a, b, c;
        let date = new Date();
        for (let posting of this.postings) {
          if (posting.date != null) {
            c = posting.date;
            a = c.slice(0, -3);
            b = date.getFullYear() + "-" + (date.getMonth() + 1);
            if (a == b) {
              array.push(posting);
            }
          }
        }
        return array;
      }
      else {
        return this.postings.filter(p => p.date == this.filterDate);
      }

    }
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
    margin: 8px;
    padding: 0;
  }
</style>
