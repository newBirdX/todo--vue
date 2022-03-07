<template>
    <footer class="footer">
        <span class="todo-count">
            <strong>{{todoNum}}</strong>
            <span v-if="todoNum<=1">item left</span>
            <span v-else>items left</span>
        </span>
        <ul class="filters">
            <li><a href="#/all" @click="filterTodo('all')" :class="{selected:view==='all'}">All</a></li>
            <li><a href="#/active" @click="filterTodo('active')" :class="{selected:view==='active'}">Active</a></li>
            <li><a href="#/completed" @click="filterTodo('completed')" :class="{selected:view==='completed'}">Completed</a></li>
        </ul>
        <button class="clear-completed" @click="clearCompleted">Clear Completed</button>
    </footer>
</template>

<script>
    export default {
        name:"footComponent",
        props:['view'],
        //计算属性
        computed:{
            todoNum(){
                return this.$parent.todoDatas.filter(value=>{
                    return !value.hasCompleted;
                }).length
            }
        },
        methods:{
            filterTodo(view){
                this.$parent.view=view;
            },
            clearCompleted(){
                this.$parent.todoDatas= this.$parent.todoDatas.filter(value=>{
                    return !value.hasCompleted
                })
            }
        }

    }
</script>

<style lang="scss" scoped>

</style>