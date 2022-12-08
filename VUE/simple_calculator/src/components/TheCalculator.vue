<template>
  <body>
    <div class="Container">
    <h1>Simple Calculator</h1>
    <input ref="calcInput" class="Number" v-model="this.calcEingabe"> 
    <div class="Buttons">
      <div>
        <simple-button @btnClick="Rechenoption" :Rechenart="'+'"></simple-button>
        <simple-button @btnClick="Rechenoption" :Rechenart="'-'">-</simple-button>
        <simple-button @btnClick="Rechenoption" :Rechenart="'*'">*</simple-button>
        <simple-button @btnClick="Rechenoption" :Rechenart="'/'">/</simple-button>
      </div>
      <button class="Ergebnis" @click="Rechenergebnis">=</button>
    </div>
  </div>
  </body>
</template>


<script>
import SimpleButton from './SimpleButton.vue'
export default {
    data() {
      return {
        calcEingabe: ""
      }
    },
    components: { SimpleButton },
    methods: {
      Rechenoption (operationType) {
        console.log(operationType)
        this.calcEingabe = this.calcEingabe + " " + operationType + " ";
        console.log(this.calcEingabe)
        this.$refs.calcInput.focus();
      },
      Rechenergebnis() {
        try {
          this.calcEingabe = eval(this.calcEingabe);
        } catch (error) {
          alert("Ungültige Eingabe")
        }
        this.$refs.calcInput.focus();
      }
    }
}
</script>


<style>
input {
  width: 94%;
  height: 40px;
  margin-bottom: 20px;
}

.Container {
  background-color: rgb(255, 124, 120);
  display: flex;
  flex-direction: column;
  padding-left: 20px;
  height: 320px;
  width: 500px;
}

div {
  display: flex;
  justify-content: center;
}

body {
  background-color: white;
  padding-top: 10px;
}

button {
  flex: 1;
  width: 100%;
  color: white;
  font-size: 2rem;
  margin-right: 20px;
  padding-top: 10px;
  padding-bottom: 10px;
}

.Ergebnis {
  width: calc(100% - 20px);
  margin-top: 20px;
}

h1 {
  text-align: center;
  color:rgb(42, 42, 45);
}

.Buttons {
  display: flex;
  flex-direction: column;
}

input[type='number']::-webkit-inner-spin-button,
input[type='number']::-webkit-outer-spin-button {
  display: none;
}

</style>