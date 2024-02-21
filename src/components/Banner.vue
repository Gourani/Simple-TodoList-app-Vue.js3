<template>
                <p>Message is: {{ message }}</p>
                <input v-model="message" placeholder="edit me" />
</template>
  
  <script>
  export default {
    data() {
      return {
        message : ""
      };
    },
    mounted() {
    if (localStorage.message) {
      this.message = localStorage.message;
    }
  },
  watch: {
    message(newName) {
      localStorage.message = newName;
    }
  }
  };
  </script>
  
  <style scoped>
  span {
    color: blue;
  }
  </style>
  