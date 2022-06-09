<template>
  <ul class="todo-list">
    <!-- completed: 完成的类名 -->
    <li :class="{completed:item.isDone}"  v-for="item in list" :key="item.id">
      <div class="view">
        <input class="toggle" type="checkbox" v-model="item.isDone"/>
        <label class="">{{item.name}}</label>
        <button class="destroy" @click="destroy(item.id)"></button>
      </div>
    </li>
  </ul>
  
</template>

<script>
// import eventBus from '../EventBus'
export default {
  props:["list"],
  methods:{
    destroy(id){
      this.$emit('destroy',id);
    }
  }
}
</script>