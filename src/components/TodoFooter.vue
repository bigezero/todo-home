<template>
  <footer class="footer">
    <span class="todo-count">剩余<strong>{{count}}</strong></span>
    <ul class="filters" @click="fn">
      <li>
        <a :class="{selected:isSel === 'all'}" href="javascript:;" @click="isSel = 'all'">全部</a>
      </li>
      <li>
        <a :class="{selected:isSel === 'no'}" href="javascript:;"  @click="isSel = 'no'">未完成</a>
      </li>
      <li>
        <a :class="{selected:isSel === 'yes'}" href="javascript:;"  @click="isSel = 'yes'">已完成</a>
      </li>
    </ul>
    <button class="clear-completed" @click="clearYes">清除已完成</button>
  </footer>
</template>

<script>
export default {
  props:['remainCount'],
  computed:{
    count(){
      return this.remainCount
    }
  },
  //点谁谁亮
  data(){
    return{
      isSel:'all' //全部"all"  已完成"yes" 未完成"no"
    }
  },
  methods:{
    fn(){
      this.$emit("changeType",this.isSel);
    },
    clearYes(){
      //纯触发事件，不传参
      this.$emit("clear")
    }
  }
}
</script>