<template>
  <header class="header">
    <h1>todos</h1>
    <input id="toggle-all" class="toggle-all" type="checkbox" v-model="isAll">
    <label for="toggle-all"></label>
    <input
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
      @keydown.enter="addNew"
      v-model="addContent"
    />
  </header>
</template>

<script>
// import eventBus from '../EventBus'
export default {
  props:["arr"],
 data(){
   return{
     addContent:""
   }
 },
 methods: {
   addNew(){
     const addNewContent = this.addContent.trim()

     if(addNewContent == 0){

       return
     }else{
       this.$emit("send",addNewContent)
       this.addContent = ""
     }
   }
 },
 computed:{
   isAll:{
    set(checked){
      this.arr.forEach(obj=>obj.isDone = checked)
    },
    get(){
      return this.arr.length !==0 && this.arr.every(obj=>obj.isDone === true)
    }
   }
 }
}
</script>