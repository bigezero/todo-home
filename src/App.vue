<template>
  <section class="todoapp">
    <!-- 除了驼峰, 还可以使用-转换链接 -->
    <TodoHeader  @send="gogogo" :arr="list"></TodoHeader>
    <TodoMain :list='showArr' @destroy="removeItem"></TodoMain>
    <TodoFooter :remainCount="showArr.length" @changeType="typeFn" @clear="clearDone"></TodoFooter>
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
      //list值取自本地，若为空，短路赋值空数组
      list:JSON.parse(localStorage.getItem('todoList')) || [],
      getSel:"all"
    }
  },
  methods: {
    gogogo(newContent){
      const newData = {}
      this.list.length>0 ? newData.id = this.list[this.list.length-1].id+1 : newData.id = 0;
      newData.name = newContent
      newData.isDone = false
      this.list.push(newData);
    },
    removeItem(idValue){
      let index = this.list.findIndex(obj=>obj.id === idValue)
      this.list.splice(index,1)
    },
    typeFn(str){
      this.getSel = str
    },
    clearDone(){
     this.list =  this.list.filter(obj => obj.isDone === false)
    }
  },
  computed:{
    showArr(){
      if(this.getSel === 'yes'){
      return this.list.filter(obj=>obj.isDone === true)
    }else if( this.getSel === 'no'){
      return this.list.filter(obj=>obj.isDone === false)
    }else{
      return this.list
    }
    }
  },
  watch:{
    list: {
      deep:true,
      handler(){
        localStorage.setItem('todoList',JSON.stringify(this.list))
      }
    }
  }
};
</script>