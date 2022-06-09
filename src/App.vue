<template>
  <section class="todoapp">
    <!-- 除了驼峰, 还可以使用-转换链接 -->
    <TodoHeader  @send="gogogo"></TodoHeader>
    <TodoMain :list='list' @destroy="removeItem"></TodoMain>
    <TodoFooter :remainCount="list.length"></TodoFooter>
  </section>
</template>

<script>
// 1.0 样式引入
import "./styles/base.css"
import "./styles/index.css"
    
import TodoHeader from "./components/TodoHeader";
import TodoMain from "./components/TodoMain";
import TodoFooter from "./components/TodoFooter";


export default {
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
  data(){
    return {
      list:[
        {id:100,name:"eat",isDone:true},
        {id:101,name:"codings",isDone:false},
        {id:102,name:"sleeping",isDone:true}]
    }
  },
  methods: {
    gogogo(newContent){
      const newData = {}
      newData.id = this.list[this.list.length-1].id+1
      newData.name = newContent
      newData.isDone = false
      this.list.push(newData);
    },
    removeItem(idValue){
      let index = this.list.findIndex(obj=>obj.id === idValue)
      this.list.splice(index,1)
    }
  }
};
</script>