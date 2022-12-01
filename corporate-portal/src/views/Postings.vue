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
    <PostingsList
        v-bind:postings="postings"
        v-bind:idSelectedItem="this.selectedPosting.id"

        @remove-posting="removePosting"
        @select-posting="selectPosting"
    />
  </div>
</template>

<script>
import PostingsList from "@/components/Postings/PostingsList"
import EditPosting from "@/components/Postings/EditPosting";
export default {
  data() {
    return {
      postings: JSON.parse(localStorage.getItem("postings")),
      tasks: JSON.parse(localStorage.getItem("tasks")),
      selectedPosting: {
        id: null,
        date: null,
        hours: null,
        id_key_task: null,    //beforeCreated  firstTask
        name: null
      }
    }
  },
  components: {
    PostingsList, EditPosting
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

      //add
      if(changedPosting.id == null) {
        const newPosting = {
          id: Date.now(),
          date: changedPosting.date,
          hours: changedPosting.hours,
          id_key_task: changedPosting.id_key_task,
          name: changedPosting.name,
        };
        if (newPosting.name == "" || newPosting.name == null) {
          newPosting.name = "Новая проводка";
        }
        if (newPosting.hours > 24) {
          newPosting.hours = 24;
        } else if (newPosting.hours <= 0) {
          newPosting.hours = 0;
        }

        let alreadyWorkedOut = 0;
        for (let posting of this.postings) {
          if (newPosting.date == posting.date) {
            alreadyWorkedOut = parseInt(alreadyWorkedOut) + parseInt(posting.hours);
          }
        }

        if (parseInt(alreadyWorkedOut) + parseInt(newPosting.hours) > 24) {
          newPosting.hours = 24 - parseInt(alreadyWorkedOut);
        }

        this.postings.push(newPosting);
      }

      //edit
      else {
        for (let currentPosting of this.postings) {
          if (changedPosting.id == currentPosting.id) {

            currentPosting.date= changedPosting.date;
            currentPosting.hours = changedPosting.hours;
            currentPosting.id_key_task = changedPosting.id_key_task;

            if (changedPosting.name == "" || changedPosting.name == null) {
              currentPosting.name = "Пустая проводка";
            }
            else {
              currentPosting.name = changedPosting.name;
            }

            if (currentPosting.hours > 24) {
              currentPosting.hours = 24;
            } else if (currentPosting.hours <= 0) {
              currentPosting.hours = 0;
            }

            let alreadyWorkedOut = 0;
            for (let posting of this.postings) {
              if (currentPosting.date == posting.date && currentPosting.id != posting.id) {
                alreadyWorkedOut = parseInt(alreadyWorkedOut) + parseInt(posting.hours);
              }
            }

            if (parseInt(alreadyWorkedOut) + parseInt(currentPosting.hours) > 24) {
              currentPosting.hours = 24 - alreadyWorkedOut;
            }

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