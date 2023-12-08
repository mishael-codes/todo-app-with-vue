<template>
  <div class="flex items-center justify-center flex-col p-4">
    <h1 class="text-amber-400 text-4xl font-semibold">CheckBook</h1>
    <div class="mt-9">
      <input v-model="newTodo" placeholder="Add a new todo" class="p-2 rounded-md my-3 bg-amber-200 text-black focus:outline-0 focus:border-amber-100 focus:border-2" />
      <button @click="addTodo" class="bg-amber-400 p-2 rounded-md">Add Todo</button>
      <ul>
        <Todo class="bg-amber-300 p-4 rounded-md" v-for="todo in todos" :key="todo.id" :todo="todo" @edit="editTodo"
          @delete="deleteTodo" @save="saveTodo" />
      </ul>
    </div>
  </div>
</template>

<script>
import Todo from './components/todo.vue';

export default {
  components: {
    Todo,
    FontAwesomeIcon,
  },
  data() {
    return {
      todos: [],
      newTodo: '',
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todos.push({ id: Date.now(), text: this.newTodo, editing: false });
        this.newTodo = '';
      }else{
        alert("Please enter a valid todo");
      }
      localStorage.setItem('todos', JSON.stringify(this.todos));
    },
    editTodo(todoId) {
      const todo = this.todos.find((t) => t.id === todoId);
      if (todo) {
        todo.editing = true;
      }
      localStorage.setItem('todos', JSON.stringify(this.todos));

    },
    deleteTodo(todoId) {
      this.todos = this.todos.filter((t) => t.id !== todoId);
      localStorage.setItem('todos', JSON.stringify(this.todos));
    },
    saveTodo() {
      localStorage.setItem('todos', JSON.stringify(this.todos));
      return `<div><p>Edited Successfully</p></div>`
    }
  },

  mounted() {
    const todos = localStorage.getItem('todos');
    if (todos) {
      this.todos = JSON.parse(todos);
    }
  },
};
</script>

<style>
ul {
  list-style: none;
  padding: 0;
}

li {
  margin-bottom: 8px;
}
</style>
