<template>
  <section class="todoapp">
    <header class="header">
      <h1>Todo</h1>
      <input type="text" placeholder="What need to be done?" class="new-todo" v-model="newTodo" @keyup.enter="addTodo">
    </header>
    <section class="main">
      <input type="checkbox" class="toggle-all" id="toggle-all" v-model="isAll">
      <label for="toggle-all"></label>
      <ul class="todo-list">
        <Item v-for="(item,index) in filterTodoDatas" :key="item.id" :todo="item" :index="index"/>
      </ul>
    </section>
    <Footer :view="view"/>
  </section>
</template>

<script>
import Item from './components/Item.vue'
import Footer from './components/Footer.vue'
  export default {
    name:"App",
    components:{Item,Footer},
    data(){
      return {
        todoDatas:[], //存储所有的todo
        newTodo:"",   //新的todo
        view:"all"   //过滤状态
      }
    },
    methods:{
      addTodo(){
        if(this.newTodo==="") return;
        let todo={};
        todo.id=new Date().getTime();
        todo.text=this.newTodo;
        todo.hasCompleted=false;
        this.todoDatas.push(todo);
        this.newTodo="";
      }
    },
    //计算属性,全选全不选
    computed:{
      isAll:{
        get(){
          return false
        },
        set(value){
          this.todoDatas.map(todo=>{
            todo.hasCompleted=value;
            return todo;
          })

        }
      },
      filterTodoDatas(){
        switch(this.view){
          case 'all':
            return this.todoDatas;
          case 'active':
            return this.todoDatas.filter(value=>{
              return !value.hasCompleted;
            })
          case 'completed':
            return this.todoDatas.filter(value=>{
              return value.hasCompleted
            })
          default:
            return this.todoDatas;
        }
      }
    }
  }
</script>

<style lang="css" scoped>

</style>