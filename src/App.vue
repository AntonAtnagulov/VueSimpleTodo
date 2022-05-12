<template>
    <div class="mainContainer">
        <form class="inputBox" @submit.prevent="addNewTodo">
            <input v-model="newTodo" name="newTodo" />
            <div class="btnBox">
                <button class="btn">ADD TODO</button>
                <button class="btn" @click="markAllDone">
                    <img src="../public/check-square.svg" width="20" />
                </button>
                <button class="btn" @click="deleteAllTodo">
                    <img src="../public/trash.svg" width="20" />
                </button>
            </div>
        </form>
        <div class="todo" v-for="(todo, index) in todos" :key="todo.id">
            <div :class="{ done: todo.done }">
                <p>{{ todo.content }}</p>
            </div>
            <div class="todoBtns">
                <button class="btn" @click="toggleDone(todo)">DONE</button>
                <button class="btn" @click="deleteTodo(index)">DELETE</button>
            </div>
        </div>
    </div>
</template>

<script>
import { ref } from 'vue';

export default {
    setup() {
        const newTodo = ref('');
        const todos = ref([]);

        function addNewTodo() {
            if (newTodo.value !== '') {
                todos.value.push({
                    id: Date.now(),
                    done: false,
                    content: newTodo.value,
                });
            }
            newTodo.value = '';
        }

        function toggleDone(todo) {
            todo.done = !todo.done;
        }

        function deleteTodo(index) {
            todos.value.splice(index, 1);
        }

        function markAllDone() {
            todos.value.forEach((el) => (el.done = true));
        }

        function deleteAllTodo() {
            todos.value = [];
        }

        return {
            todos,
            newTodo,
            addNewTodo,
            toggleDone,
            deleteTodo,
            markAllDone,
            deleteAllTodo,
        };
    },
};
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}

.mainContainer {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.inputBox {
    display: flex;
    justify-content: space-around;
    align-items: center;
    width: 50%;
    padding: 15px;
    background-color: #ffffff3c;
    border-radius: 12px;
    margin: 1%;
}

.inputBox input {
    border: 1px solid #ffffffb0;
    font-size: 20px;
    color: #ffffff;
    background-color: #ffffff00;
    outline: none;
    width: 50%;
    padding: 10px 20px;
    border-radius: 12px;
}

.btn {
    width: 100px;
    height: 50px;
    border: none;
    color: #ffffff;
    background-color: #154135;
    border-radius: 12px;
}

.btn:hover {
    background-color: #154135ab;
}

.todo {
    display: flex;
    justify-content: space-between;
    width: 70%;
    background-color: #ffffff3c;
    border-radius: 12px;
    margin: 1%;
    padding: 5px 20px;
}
.todo p {
    user-select: none;
    color: #ffffff;
    font-size: 20px;
}

.todoBtns {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 210px;
}

.btnBox {
    display: flex;
    justify-content: space-between;
    width: 350px;
    background-color: #ffffff3c;
    border-radius: 12px;
    padding: 10px;
}

.done p {
    color: rgb(131, 217, 177);
    text-decoration: line-through;
}
</style>
