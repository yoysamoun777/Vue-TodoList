

<template>
  <div class="h-[25rem] overflow-auto bg-teal-500 border rounded-xl w-[80%] md:w-[60%] lg:w[40%] p-5 absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 bg-gradient-to-r from-cyan-400 to-blue-800">
    <h1 class="text-lg font-bold mb-2">Todo List</h1>
  
    <div>
      <input type="text" placeholder="title ... "
       class="lg:w-[93%] mr-2 px-5 py-1 rounded-xl bg-transparent border placeholder:text-gray-200 outline-none"
       v-model="titleInput">
      <button class=" bg-gradient-to-l from-indigo-500 via-purple-500 to-pink-500 rounded-xl px-2 py-1 active:bg-pink-500 ml-0"
      @click="addTodo">Add</button>
    </div>

    <div v-for="todo in data">
      <div class="border px-5 py-1 rounded-xl mt-2 cursor-pointer hover:bg-gray-700 transition-all justify-between flex items-center">
        <h1>{{todo.title}}</h1>
      <div>
        <button class="bg-blue-500 px-2 py-1 rounded-xl">Doned</button>
        <button class="ml-2 bg-red-500 px-1 py-1 rounded-xl">Delete</button>
      </div>
    </div>

    </div>
    
  </div>
</template>

<script>
import { ref } from 'vue';

  export default {
    setup() {

      const titleInput = ref("");

      const data = ref();
      const getAll = () => {
        data.value = JSON.parse(localStorage.getItem('todo'));
      }
      getAll();

      

      const addTodo =() => {
         if (!titleInput.value) return alert("Please input something");
         const items = JSON.parse(localStorage.getItem("todo"));
         const existed = items?.find(item => item.title === titleInput.value);
         if(existed) return alert("Existed Todo");

         if(items) {
          localStorage.setItem('todo', JSON.stringify([...items, { title: titleInput.value, doned: false }]))
         }else{
          localStorage.setItem('todo', JSON.stringify([{ title: titleInput.value, doned: false }]))
         }
         titleInput.value = "";
         getAll();

      }
      

      return {
        data,
        titleInput,
        addTodo,
      
      }
    }
  }
</script>
