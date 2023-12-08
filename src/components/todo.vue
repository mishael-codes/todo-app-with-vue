<template>
  <div class="bg-amber-300 my-5">
    <li v-if="todo.editing == false">
      <p class="mb-3">{{ todo.text }}</p>
      <hr class="w-full h-1 my-3 border-0 rounded dark:bg-[#090909]">
      <div class="w-full flex">
        <button @click="editTodo"
          class="bg-[#090909] w-fit text-amber-300 rounded-md mr-3 py-1 px-3 font-semibold flex">Edit <img src="../icons/edit.svg" alt=""></button>
        <button @click="deleteTodo" class="bg-red-800 w-fit text-white rounded-md py-1 px-3 font-semibold">Delete</button>
      </div>
    </li>
    <li v-else>
      <input type="text" v-model="editedText"
        class="p-1 bg-amber-200 rounded-md focus:outline-0 focus:border-amber-100 focus:border-4">
      <hr class="w-full h-1 my-3 border-0 rounded dark:bg-[#090909]">
      <div>
        <button @click="saveTodo"
          class="bg-[#090909] w-fit text-amber-300 rounded-md mr-3 py-1 px-3 font-semibold">Save</button>
        <button @click="deleteTodo" class="bg-red-800 w-fit text-white rounded-md py-1 px-3 font-semibold">Delete</button>
      </div>
    </li>
  </div>
</template>

<script>
import editBtn from '../icons/edit.svg';

export default {
  props: ['todo'],
  data() {
    return {
      editedText: this.todo.text
    }
  },
  methods: {
    editTodo() {
      this.$emit('edit', this.todo.id);
    },
    deleteTodo() {
      this.$emit('delete', this.todo.id);
    },
    saveTodo() {
        this.$emit('save', this.todo.id, this.editedText);
    }  
  },
};
</script>
