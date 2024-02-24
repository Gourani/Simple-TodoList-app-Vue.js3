<script  setup>
import { ref, reactive, watch, computed, onMounted } from "vue";
import Banner from "./components/Banner.vue";
let todoItem = reactive({
  body: "",
  category: "",
  checked: false,
});
let list_of_todos = ref([]);
const categories = ref(["business","personal"])
const doThis = (todo) => {
  const todo_ = {
    body: todo.body,
    category: todo.category,
    checked: todo.checked,
  };

  list_of_todos.value.push(todo_);
  todoItem.body=""
  
  todoItem.category=""
  todoItem.checked= false
  
};

const deleteTodo = (id) => {
  list_of_todos.value.splice(id, 1);
};
onMounted(() => {
  if (localStorage.list_of_todos) {
    list_of_todos.value = JSON.parse(localStorage.list_of_todos);
    // console.log(list_of_todos.value)
  }
});
const isDisabled = computed(() => {
  if (
    todoItem.body !== "" &&
    ["business", "personal"].includes(todoItem.category)
  ) {
    return false;
  } else {
    return true;
  }
});
watch(
  list_of_todos,
  async (newvalue, oldvalue) => {
    newvalue = JSON.stringify(newvalue);
    localStorage.list_of_todos = newvalue;
  },
  {
    deep: true,
  }
);
</script>

<template>
  <Banner />
  <span>Create a todo</span>
  <div>
    <span class="makesmall"> What's on your todo list ?</span>
  </div>
  <div>
    <input
      type="text"
      v-model="todoItem.body"
      placeholder="Write something ..."
      class="card"
    />
  </div>
  <div>
    <span class="makesmall"> Pick a category ...</span>
  </div>
  <div class="hold_category">
    <div v-for="cat in categories" class="category_card"><br>
      <div class="container">
        <input
          type="radio"
          id="1"
          :value="cat"
          

          v-model="todoItem.category"
          name="radio"
        />
      </div>
      <p>{{cat}}</p>
    </div>
   
  </div>
  <div>
    <button v-on:click="doThis(todoItem)" :disabled="isDisabled" class="add">
      Add todo
    </button>
  </div>

  <h3 class="todo_list">Todo List</h3>
  <div class="scroll_list">
    <div class="todo" v-for="(item, key) in list_of_todos" :key="key">
      <div>
        <input
          type="checkbox"
          name="category"
          id="busi_or_perso"
          :value="item.category"
          v-model="item.checked"
        />
        <del v-if="item.checked">{{ item.body }} </del>
        <span v-else> {{ item.body }} </span>
      </div>
      <div>
        <button @click="deleteTodo(key)">Delete</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.makesmall {
  font-size: small;
}
.category_card {
  width: 49%;
  height: 100px;
  text-align: center;
  background-color: white;
  box-shadow: 3px 3px 2px 1px rgba(147, 147, 147, 0.2);
  border-radius: 10px;
}

.hold_category {
  display: flex;
  justify-content: space-between;
  margin: 15px 0;
}

/* The container */
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  
  font-size: 22px;

  height:30px;
}

.container input[type="radio"][value="business"]{
  height:20px;
  width: 20px;
  accent-color: var(--business);

}
.container input[type="radio"][value="personal"]{
  height:20px;
  width: 20px;
  accent-color: var(--personal);

}
.add {
  background-color: var(--primary);
  width: 100%;
  padding: 10px 25px;
  border-radius: 10px;
  color: rgb(255, 255, 255);
  border: 0;
}

.todo_list {
  margin: 10px;
}

.todo {
  background-color: white;
  margin-bottom: 5px ;
  padding: 10px 20px;
  display: flex;
  justify-content: space-between;
  text-transform: capitalize;
}
.todo input[type="checkbox"] {
  border-radius: 50%;
  margin-right: 10px;
  height:20px;
  width:20px;
 
}

.todo input[type="checkbox"][value='business'] {
  accent-color: var(--business);

}

.todo input[type="checkbox"][value='personal'] {
  accent-color: var(--personal);

}
.todo div button {
  font-size: small;
  padding: 10px;
  border: 0;
  border-radius: 10px;
  background-color: var(--danger);
  color: white;
}
.scroll_list{
  height:300px;
  overflow-y: auto;
  overflow-x: hidden;
}

.category_card p {
  font-size: medium;
}
</style>
