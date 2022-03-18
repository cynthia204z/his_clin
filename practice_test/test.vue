<template>
  <div>
    <input v-model="newText" @input="updateChange"/>
    <slot/>
  </div>
</template>
<script>
module.exports = {
  name: 'test',
  props: {
    text: String
  },
  data(){
    return{
      newText: 'Hello World!'
    }
  },
  methods:{
    updateChange(){
      this.$emit('update:text', this.newText)
    }
  }
}
</script>
<style scoped>
</style>
