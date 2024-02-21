<script setup>
import Banner from './components/Banner.vue'
</script>
<script>
export default {
  data(){
    return{
      item:"items"
    }
  }
}

</script>
<template>

    <Banner />
    <h2>Create a todo</h2>
    <span>What's on your todo list ?</span>
    <span>e.g. make a video</span>
    <span>pick a category</span>
    <input type="radio" name="category" id="business"  />Business
    <input type="radio" name="category" id="personal"  />Personal
    <button>
      Add todo
    </button>
    <h3>Todo List</h3>
    <div >
      <input type="radio" name="category" id="busi_or_perso"/>
      {{ item }}
      <button>
        Delete
      </button>
    </div>
</template>

<style scoped>

</style>
