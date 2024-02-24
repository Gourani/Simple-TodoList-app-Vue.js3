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


<template>
          <div>
            <h1>What's Up, <input v-model="message" placeholder="edit me" /></h1>
          </div>

                
</template>
  
  
  
  <style scoped>
  h1{
    font-weight:bold;
  }
 input{
  font-weight:bold;
  background-color: #f2f2f2;
  border:none;
  text-transform: capitalize;
}
div{
  margin-bottom: 20px;
}
input:focus{
  outline: none;
}
  </style>
  