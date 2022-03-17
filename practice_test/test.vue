<template>
  <div>
    <input v-model="text"/>
    <div class="colorbox">{{text}}</div>
  </div>
</template>
<script>
module.exports = {
  name: 'test',
  data(){
    return{
      text: '123456'
    }
  }
}
</script>
<style scoped>
.colorbox{
  background-color:black;
  color: gray;
  height: 30px;
  line-height: 30px;
  text-align: center;
  padding: 0 10px;
}
</style>
