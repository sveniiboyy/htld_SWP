<template>
    <div class="wrapper">
      <div class="input-container" v-if="this.Lernen === false">
        <h1>Deine eigene Lernplattform</h1>
        <div class="input-group">
          <label for="NewWord">Neues Wort:</label>
          <input type="text" id="NewWord" v-model="this.newWord"/>
        </div>
        <div class="input-group">
          <label for="NewTranslation">Übersetzung:</label>
          <input type="text" id="NewTranslation" v-model="this.newTranslation" />
        </div>
        <div class="button-group">
          <button @click="Lernen = true">Lernen</button>
          <button @click="addWord">Wort hinzufügen</button>
        </div>
      </div>
      <div class="lernen-wrapper" v-if="this.Lernen === true">
            <h1>Deine Vokabeln</h1>
            <WordsList></WordsList>
            <button class="Zurück" @click="()=>{this.Lernen=false}">Zurück</button>
      </div>
    </div>
</template>
    
    <script>
    import WordsList from './WordsList.vue';
    
    export default {
      data() {
        return {
          newWord: '',
          newTranslation: '', 
          Lernen: false,
        }
      },
      methods: {
        addWord() {
          if(this.newWord === '' | this.newTranslation === '') {
            return alert("Bitte geben Sie in beide Eingabefelder etwas ein!");
          }
          fetch("https://vokabel-app-7df0a-default-rtdb.europe-west1.firebasedatabase.app/Words.json",{method:"POST", body:JSON.stringify({newWord:this.newWord, newTranslation:this.newTranslation})})
          this.newWord = '';
          this.newTranslation = '';
          document.getElementById('NewWord').focus();
          document.getElementById('NewWord').select();
        },
      },
      components: {
        WordsList
      }
    }
    </script>


    <style>
    body,
    html {
      background-color: black;
      overflow: hidden;
    }


    h1 {
      margin-top: -10px;
      margin-bottom: 40px;
    }
    
    .wrapper {
      background-color: darkcyan;
      padding-top: 30px;
      padding-bottom: 30px;
      padding-left: 100px;
      padding-right: 100px;
      border-radius: 15px;
      transform: scale(1.2);
    }
    
    .input-container {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      color: white;
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    }
    
    .input-group {
      display: flex;
      align-items: center;
      text-align: right;
      margin-bottom: 10px;
      justify-content: space-between;
      width: 70%;
    }
    
    
    .button-group {
      display: flex;
      justify-content: center;
      text-align: center;
      justify-content: space-around;
    }
    
    .button-group button {
      margin-left: 10px;
      margin-top: 20px;
      width: 110px;;
      height: 50px;
      background-color: cyan;
      border-color: blue;
      font-weight: bold;
    }
    
    .button-group button:hover {
      background-color: blueviolet;
      color:white;
      font-size: 14px;
      font-weight: bold;
      transition: all 0.3s;
    }
    
    .Zurück {
      width: 70px;;
      height: 30px;
      background-color: cyan;
      border-color: blue;
      font-weight: bold;
      margin-top: 30px;
    }

    .Zurück:hover {
      background-color: blueviolet;
      color:white;
      font-size: 14px;
      font-weight: bold;
      transition: all 0.3s;
    }

    </style>