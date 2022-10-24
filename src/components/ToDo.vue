<template>
    <div>
        <form v-on:submit.prevent="handleTodoSubmit" id="todo-form" class="todos-form">
            <input v-model="newTodo" required type="text" placeholder="할 일을 입력하고 엔터를 눌러주세요." class="todos-input"/>
        </form>
        <ul id="todo-list" class="todos font-color">
            <li v-for="todo in toDos" v-bind:key="todo.id" :id="todo.id">
                <span>{{ todo.text }}</span>
                <button v-on:click="deleteTodo">❌</button>
            </li>
        </ul>
    </div>
</template>

<script>
const TODOS_KEY = "toDos";
export default {
    data: function () {
        return {
            newTodo: "",
            toDos: []
        }
    },
    mounted: function () {
        this.getTodos();
    },
    methods: {
        handleTodoSubmit: function () {
            const newTodoObj = {
                text: this.newTodo,
                id: Date.now()
            };

            this.toDos.push(newTodoObj);
            this.saveTodos();
            this.newTodo = "";
        },
        saveTodos: function  () {
            localStorage.setItem(TODOS_KEY, JSON.stringify(this.toDos));
        },
        deleteTodo: function (event) {
            const li = event.target.parentElement;
            this.toDos = this.toDos.filter((item) => this.toDosFilter(item.id, parseInt(li.id)));
            this.saveTodos();
        },
        toDosFilter: function (toDosId, liId) {
            return toDosId !== liId;
        },
        getTodos: function () {
            const savedToDos = localStorage.getItem(TODOS_KEY);

            if (savedToDos !==  null) {
                const parsedToDos = JSON.parse(savedToDos);
                this.toDos = parsedToDos;
            }
        }
    }
}
</script>

<style>
    
</style>