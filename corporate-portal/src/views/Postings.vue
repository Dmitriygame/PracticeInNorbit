<template>
  <div>
    <h2>Проводки</h2>
    <hr>
    <EditPosting
        v-bind:selectedPosting="this.selectedPosting"
        v-bind:tasks="this.tasks"

        @edit-posting="editPosting"
    />
    <hr>
    <FilterPostings
        @set-filter="setFilter"
    />
    <hr>
    <PostingsList
        v-bind:postings="postings"
        v-bind:tasks="this.tasks"
        v-bind:idSelectedItem="this.selectedPosting.id"
        v-bind:filterDate="this.filterDate"

        @remove-posting="removePosting"
        @select-posting="selectPosting"
    />
  </div>
</template>

<script>
import PostingsList from "@/components/Postings/PostingsList";
import EditPosting from "@/components/Postings/EditPosting";
import FilterPostings from "@/components/Postings/FilterPostings";

export default {
  data() {
    return {
      postings: JSON.parse(localStorage.getItem("postings")),
      tasks: JSON.parse(localStorage.getItem("tasks")),
      selectedPosting: {
        id: null,
        date: null,
        hours: null,
        id_key_task: null,
        name: null
      },
      filterDate: "all"
    }
  },
  components: {
    PostingsList, EditPosting, FilterPostings
  },

  beforeMount() {
    this.selectedPosting.id_key_task = this.firstTaskId();
  },

  methods: {
    removePosting(id) {
      this.postings = this.postings.filter(p => p.id != id);
      localStorage.setItem("postings", JSON.stringify(this.postings));
    },

    editPosting(changedPosting) {

      if (changedPosting.name == "" || changedPosting.name == null) {
        changedPosting.name = "Пустая проводка";
      }

      if (changedPosting.date == null || changedPosting.date == "") {
        let dateNow = new Date();
        let m = dateNow.getMonth() + 1;
        if (m < 10)
          m = "0" + m;
        let d = dateNow.getDate();
        if (d < 10)
          d = "0" + d;
        changedPosting.date = dateNow.getFullYear() + "-" + m + "-" + d;
      }

      if (changedPosting.hours > 24) {
        changedPosting.hours = 24;
      }
      else if (changedPosting.hours <= 0) {
        changedPosting.hours = 0;
      }

      let alreadyWorkedOut = 0;
      for (let posting of this.postings) {
        if (changedPosting.date == posting.date && changedPosting.id != posting.id) {
          alreadyWorkedOut = parseInt(alreadyWorkedOut) + parseInt(posting.hours);
        }
      }

      if (parseInt(alreadyWorkedOut) + parseInt(changedPosting.hours) > 24) {
        changedPosting.hours = 24 - alreadyWorkedOut;
      }

      //add
      if(changedPosting.id == null) {
        const newPosting = {
          id: Date.now(),
          date: changedPosting.date,
          hours: changedPosting.hours,
          id_key_task: changedPosting.id_key_task,
          name: changedPosting.name,
        }

        this.postings.push(newPosting);
      }

      //edit
      else {
        for (let currentPosting of this.postings) {
          if (changedPosting.id == currentPosting.id) {

            currentPosting.name = changedPosting.name;
            currentPosting.date = changedPosting.date;
            currentPosting.hours = changedPosting.hours;
            currentPosting.id_key_task = changedPosting.id_key_task;

            break;
          }
        }
      }

      this.selectedPosting.id = null;
      this.selectedPosting.date = null
      this.selectedPosting.hours = null;
      this.selectedPosting.id_key_task = this.firstTaskId();
      this.selectedPosting.name = null;

      localStorage.setItem("postings", JSON.stringify(this.postings));
    },

    setFilter(filterDate) {
      this.filterDate = filterDate;
    },

    firstTaskId() {
      for (let task of this.tasks) {
        if (task.active == true) {
          return task.id;
        }
      }
    },

    selectPosting(posting) {
      this.selectedPosting.id = posting.id;
      this.selectedPosting.date= posting.date;
      this.selectedPosting.hours= posting.hours;
      this.selectedPosting.name = posting.name;
      this.selectedPosting.id_key_task= posting.id_key_task;
    }
  }
}
</script>