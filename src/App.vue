<script>
let id = 0;

export default {
  data() {
    return {
      newEntryName: "",
      randomized: false,
      entries: [],
    };
  },
  computed: {
    getList() {
      if (this.randomized) {
        const randomNumList = this.entries.map((e) => {
          return Object.assign({}, e, { randomNum: Math.random() });
        });
        // Console log every entry's assigned random number in list
        const sortedRandomNumList = randomNumList.sort(
          (a, b) => a.randomNum - b.randomNum
        );
        console.log(sortedRandomNumList);
        // return sorted list
        return sortedRandomNumList;
      }
      // default return non-sorted list
      return this.entries;
    },
  },
  methods: {
    addEntry() {
      const newEntry = { id: id++, name: this.newEntryName, randomNum: null };
      this.entries.push(newEntry);
      // log new entry
      console.log("New Entry: ", newEntry);
      this.newEntryName = "";
    },
    removeEntry(entry) {
      this.entries = this.entries.filter((e) => e.id !== entry.id);
    },
    resetList() {
      this.entries = [];
      this.randomized = false;
    },
  },
};
</script>

<template>
  <form @submit.prevent="addEntry">
    <input v-model="newEntryName" />
    <button>Add Entry</button>
  </form>
  <ul>
    <li v-for="entry in getList" :key="entry.id">
      <span>{{ entry.name }}</span>
      <button v-if="!randomized" @click="removeEntry(entry)">X</button>
    </li>
  </ul>
  <button v-if="!randomized && entries.length > 1" @click="randomized = true">
    {{ "Randomize!" }}
  </button>
  <button v-if="randomized" @click="resetList()">
    {{ "Reset List" }}
  </button>
</template>

<style>
/* TODO */
</style>
