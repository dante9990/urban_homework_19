<template>
    <li :class="{completed: task.completed}" class="todo__item">
        <span @click="$emit('toggle-completion', task)" class="todo__text">
            {{ task.text }}
        </span>
        <button @click="$emit('remove-task', task.id)" class="remove__button">Удалить</button>
    </li>
    
</template>

<script>
export default {
    name: 'TodoItem',
    props: ['task'],
    emits: ['toggle-completion', 'remove-task'],
}
</script>

<style scoped>
.todo__item {
    display: flex;
    justify-content: space-between;
    padding: 10px;
    border-bottom: 1px solid #ddd;
    color: #fff;
}

.completed .todo__text {
    text-decoration: line-through;
    color: #aaa;
}

.todo__text {
    cursor: pointer;
    align-self: center;
    font-size: 18px;
}

.remove__button {
    background-color: #f44336;
    color: white;
    border: none;
    border-radius: 4px;
    padding: 20px 20px;
    cursor: pointer;
    transition: background-color 0.3s;
}

.remove__button:hover {
    background-color: #e53935;
}
</style>