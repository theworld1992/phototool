<template>
  <div class="list" >
    <div >
      <span class="title">{{name}}</span>
      <span>：</span>
      <input type="text" class="input" v-model.number="value" @keydown.13="run">
    </div>
    <input type="range" max="100" min="0" v-model.number="value" @change="run">
  </div>
</template>

<script>
 export default {
  data:function(){
   return {
     value:0,
   }
  },
  methods:{
    run:function(){ 
      this.$emit("parent",this.name,this.value)
    }
  },
  watch:{
    value:function(newvalue){
      if(newvalue>100){
        this.value = 100
      }else if(newvalue<0){
        this.value = 0
      }
    }
  },
  props:["name"]
 }
</script>

<style scoped>
  .list {
    height: 70px;
    line-height: 40px;
    text-align: center;
    border-top: 2px solid rgb(211,211,211); 
  }
  .input {
    width: 30px;
  }
  .title {
    font-weight: 700;
  }
</style>
