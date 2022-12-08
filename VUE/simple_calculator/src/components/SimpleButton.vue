<template>
  <button @click="clickEvent">{{this.Rechenart}}</button>
</template>

<script>
export default {
props: {Rechenart:{type:String,required:true}},
emits: ["btnClick"],
  methods: {
    clickEvent() {
      this.$emit('btnClick', this.Rechenart)
    }
  }
}
</script>

<style>
button {
  background-color: rgb(215, 171, 87);
}
</style>