<template>
  <div>
    <add-word></add-word>
  </div>
</template>

<script>
import AddWord from "./components/AddWord.vue";

export default {
  data() {
    return {
      words: []
    }
  },
  methods: {
    addWord(word) {
      this.words.push(word)
    }
  },
  components: {
    AddWord
  }
}
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  margin-top: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  overflow: hidden;
  margin: 0;
}
</style>
