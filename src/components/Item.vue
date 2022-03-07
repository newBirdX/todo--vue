<template>
    <li :class="{completed:todo.hasCompleted,editing:todo===editedTodo}">
        <div class="view">
            <input type="checkbox" class="toggle" v-model="todo.hasCompleted">
            <label @dblclick="editTodo">{{todo.text}}</label>
            <button class="destroy" @click="delTodo(todo.id)"></button>
        </div>
        <input type="text" class="edit"
        v-model.trim="editedTodo.text" 
        v-focus
        @keyup.enter="doneTodo"
        @blur="doneTodo"
        @keyup.esc="cancelTodo(index)"
        >
    </li>
</template>

<script>
    export default {
        name:"itemComponent",
        props:['todo','index'],
        data(){
            return {
                editedTodo:"", //存放todo
                value:"" ,//存放初始todo的值
            }
        },
        methods:{
            //删除todo
            delTodo(id){
                this.$parent.todoDatas=this.$parent.todoDatas.filter(value=>{
                    return !(value.id===id)
                })
            },
            //双击todo
            editTodo(){
                this.value=this.todo.text;
                this.editedTodo=this.todo;
            },
            doneTodo(){
                this.editedTodo=""
            },
            cancelTodo(index){
                this.$parent.todoDatas[index].text=this.value; //把双击进入编辑后的存的初始todo赋值给父组件中对应的todo
                this.editedTodo="";
            }
        },
        directives:{
            focus(el,value){
                //有问题！！！！！
                // console.log("el",el);
                // console.log("value",value);
                el.focus();
            }
        }
    }
</script>

<style lang="scss" scoped>

</style>