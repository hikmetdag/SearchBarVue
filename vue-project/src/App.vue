<script setup>
import userData from './clients.json'
import { ref } from 'vue'
//Initial value of input is null
let input = ref('')
function filteredList() {
  //Frist 10 names will be initially presented, 
  if (!input.value) {
    return userData.slice(0, 10)
  }
  return userData
    .filter((item) =>
      `${item.first_name} ${item.last_name} ${item.origin}`
        .toLowerCase()
        .includes(input.value.toLowerCase())
    )
    .slice(0, 10)
}
</script>

<template>
  <div class="wrapper">
    <input type="text" v-model="input" placeholder="Search clients..." />
    <div class="item" v-for="item in filteredList()" :key="item">
      <p>
        {{ `${item.first_name} ${item.last_name}(${item.origin})` }}
      </p>
    </div>
    <div class="item error" v-if="input && !filteredList().length">
      <p>No results found!</p>
    </div>
  </div>
</template>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: 'Montserrat', sans-serif;
}

body {
  display: flex;
  flex-direction: column;
  align-items: center;
  min-height: 100vh;
  background-color: rgb(234, 242, 255);
  padding: 40px;
}

input {
  width: 350px;
  padding: 10px 45px;
  background: white;
  font-size: 16px;
  border: none;
  border-radius: 5px;
  margin-top: 10px;
  box-shadow:
    rgba(50, 50, 93, 0.25) 0px 2px 5px -1px,
    rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
}

.item {
  width: 250px;
  margin: 10px;
  padding: 10px;
  color: white;
  border-radius: 5px;
  background-color: rgb(97, 62, 252);
  cursor: pointer;
}

.wrapper {
  padding-top: 10vh;
  width: 500px;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  overflow-y: auto;

  .error {
    background-color: tomato;
  }
}
</style>
