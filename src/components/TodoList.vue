<template>
    <div class="todo-list__container">
        <form @submit.prevent="addNewTask" class="todo-list__form">
            <input type="text" v-model="newTaskInput" placeholder="Введите задачу" class="todo-list__input">
            <button type="submit" class="todo-list__button">Добавить</button>
        </form>
        <p v-if="tasks.length === 0">Задач нет!</p>
        <ul class="todo-list">
            <TodoItem v-for="task in tasks" :key="task.id" :task="task" @remove-task="$emit('remove-task', $event)"
                @toggle-completion="$emit('toggle-completion', $event)" />
        </ul>
    </div>
</template>

<script>
import { ref } from 'vue';
import TodoItem from './TodoItem.vue';

export default {
    name: 'TodoList',
    components: { TodoItem },
    props: ['tasks'],
    emits: ['add-task', 'remove-task', 'toggle-completion'],
    setup(_, { emit }) {
        const newTaskInput = ref('');

        const addNewTask = () => {
            if (newTaskInput.value.trim() !== '') {
                emit('add-task', newTaskInput.value);
                newTaskInput.value = '';
            }
        };

        return { newTaskInput, addNewTask }
    }
}
</script>

<style scoped>
.todo-list__container {
    background: #443434;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.todo-list__form {
    display: flex;
    gap: 10px;
    margin-bottom: 20px;
}

.todo-list__input {
    flex: 1;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 4px;
}

.todo-list__button {
    background-color: #4caf50;
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s;
}

.todo-list__button:hover {
    background-color: #45a049;
}

.todo-list {
    list-style: none;
    padding: 0;
}

p {
    color: #fff;
}
</style>