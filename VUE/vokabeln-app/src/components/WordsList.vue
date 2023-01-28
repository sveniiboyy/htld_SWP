<template>
    <div>
      <ul>
        <li v-for="word in words" :key=word.key>
          <div class="container">
            <div class="left">{{ word.name }}</div>
            <div class="right"> {{ word.translations}}</div>
          </div>
          <button class="Delete" @click="deleteWord(word.key)">Löschen</button>
        </li>
      </ul>
    </div>
  </template>
  <script>
  export default {
    data() {
      return {
        words: []
      }
    },
    methods: {
      deleteWord(key) {
          fetch(`https://vokabel-app-7df0a-default-rtdb.europe-west1.firebasedatabase.app/Words/${key}.json`,{method:"DELETE"}).then((res) => {console.log(res); this.fetchData()})
          console.log(this.words)
        },
    async fetchData() {
      let response = await fetch("https://vokabel-app-7df0a-default-rtdb.europe-west1.firebasedatabase.app/Words.json");
      let data = await response.json();
      let results = [];
      if(!data) {
        this.words = results;
        return;
      }
      let newData = Object.entries(data);
   
        for(let i = 0; i < newData.length; i++) {
        results.push({
          name: newData[0][1].newWord,
          translations: newData[0][1].newTranslation,
          key: newData[0][0]
        })
      }
      
      this.words = results;
      console.log(this.words);
    }
  },
  async created () {
      this.fetchData();
    }

}
  </script>

<style>
h2 {
  margin-top: 350px;
  display: flex;
  align-items: center;
  justify-content: center;
}

ul {
  margin: 0px;
  margin-top: -10px;
  padding: 0px;
  padding-bottom: 30px;
  height:50vh;
  width:50vw;
  overflow-y:scroll;
  -ms-overflow-style: none;
}
ul::-webkit-scrollbar {
  display: none;
}

li {
  list-style: none;
  background-color: white;
  color: black;
  padding-left: 30px;
  padding-right: 30px;
  padding-top: 15px;
  padding-bottom: 15px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  display: flex;
  flex-direction: row;
}

li:nth-child(1) {
  border-top-left-radius: 20px;
  border-top-right-radius: 20px;
}

li:last-child {
  border-bottom-left-radius: 20px;
  border-bottom-right-radius: 20px;
}

.container {
  display: flex;
  justify-content: space-between;
  width: 40vw;
  margin-right: 40px;
}

.Delete  {
      width: 65px;;
      height: 25px;
      background-color: white;
      border-color: black;
    }

.Delete:hover {
      background-color: black;
      color:white;
      font-style: italic;
      transition: all 0.3s;
      border-color: white;
}

</style>

