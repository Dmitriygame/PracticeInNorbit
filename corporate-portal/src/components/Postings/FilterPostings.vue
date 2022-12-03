<template>
  <button v-on:click="this.filterDate='all', this.$emit('set-filter', this.filterDate)">За всё время</button>
  <button v-on:click="this.filterDate='month', this.$emit('set-filter', this.filterDate)">За месяц</button>
  <button v-on:click="this.filterDate=this.date, this.$emit('set-filter', this.filterDate)">За выбранный день</button>
  <input type="date" v-model="this.date">
</template>

<script>
export default {
  data() {
    return {
      filterDate: "all",   //or "month" or day (for example "2022-12-01")
      date: null
    }
  }
}

</script>