<template>
  <div id="app" class="app__container">
    <h1 class="app__title">To-do List</h1>
    <TodoList :tasks="tasks" @add-task="addTask" @remove-task="removeTask" @toggle-completion="toggleCompletion" />
  </div>
</template>

<script>
import { ref } from 'vue';
import TodoList from './components/TodoList.vue';


export default {
  name: 'App',
  components: {
    TodoList
  },
  setup() {
    const tasks = ref([]);

    const addTask = (newTask) => {
      tasks.value.push({
        id: Date.now(),
        text: newTask,
        completed: false
      });
    };

    const removeTask = (id) => {
      tasks.value = tasks.value.filter(task => task.id !== id);
    };

    const toggleCompletion = (task) => {
      task.completed = !task.completed;
    };

    return { tasks, addTask, removeTask, toggleCompletion }
  }
};
</script>

<style scoped>
.app__container {
  font-family: Arial, sans-serif;
  text-align: center;
  background-color: #b37f7f;
  padding: 20px;
  border-radius: 10px;
  max-width: 600px;
  margin: 40px auto;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.app__title {
  font-size: 2.5rem;
  color: #333;
  margin-bottom: 20px;
}
</style>
