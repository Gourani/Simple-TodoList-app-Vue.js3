<script  setup>
import { ref,reactive ,watch,computed, onMounted} from 'vue';
import Banner from './components/Banner.vue';
let todoItem = reactive(
  {
    body:"",
    category:"",
    checked:false,
  }
)
let list_of_todos = ref([])

const doThis = (todo) => {
  const todo_ = {
    "body":todo.body,
    "category":todo.category,
    "checked":todo.checked,
  }
  list_of_todos.value.push(todo_);
}

const deleteTodo = (id) => {
  console.log(id)
  list_of_todos.value.splice(id,1)
}
onMounted(()=>{
  console.log("on mounted")
  if (localStorage.list_of_todos){
    console.log("here")
    console.log(JSON.parse(localStorage.list_of_todos))
    list_of_todos.value = JSON.parse(localStorage.list_of_todos)
   // console.log(list_of_todos.value)
  }
})
const isDisabled = computed(()=>{
  if (todoItem.body !== "" && ["business", "personal"].includes(todoItem.category)){
    return false
  }else {
    return  true
  }
})
watch(list_of_todos, async (newvalue, oldvalue) => {
      console.log(newvalue)
      newvalue = JSON.stringify(newvalue)
      localStorage.list_of_todos = newvalue;
      console.log("watch")
},{
  deep:true
})

</script>

<template>

    <Banner />
    <h2>Create a todo</h2>
    <span>What's on your todo list ?</span>
    <input type="text" v-model="todoItem.body" placeholder="Write something for god sake">
    <span>pick a category</span>
    <input type="radio" name="category" id="1" value="business" v-model="todoItem.category" />Business
    <input type="radio" name="category2" id="2" value="personal" v-model="todoItem.category" />Personal
    <button v-on:click="doThis(todoItem)" :disabled='isDisabled'>
      Add todo
    </button>
    <h3>Todo List</h3>
    <div v-for="(item,key) in list_of_todos" :key="key">
      <input type="checkbox" name="category" id="busi_or_perso" value="completed" v-model="item.checked" />
      {{ item.body }}
      <button @click="deleteTodo(key)">
        Delete
      </button>
    </div>
</template>

<style scoped>

</style>
