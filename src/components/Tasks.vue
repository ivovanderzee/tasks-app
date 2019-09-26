<template>
  <div class="hello">
    <div class="holder">
      <form @submit.prevent="addTask">
        <input type="text" placeholder="Enter a new task" v-model="task" />
      </form>

      <ul>
        <transition-group
          name="list"
          enter-active-class="animated slideInLeft"
          leave-active-class="animated slideOutRight"
        >
          <li v-for="task in tasks" v-bind:key="task.id">
            {{ task.name }}
            <button class="deleteBtn" @click="deleteTask(task.id)">delete</button>
          </li>
        </transition-group>
      </ul>

      <p v-if="tasks.length >= 1">You have {{ tasks.length }} tasks to do</p>
      <p v-else>You have nothing to do</p>
    </div>
  </div>
</template>

<script>
import { extend } from "vee-validate";
import { required } from "vee-validate/dist/rules";

let counter = 0;

export default {
  name: "Tasks",

  data() {
    return {
      task: "",
      tasks: []
    };
  },

  methods: {
    addTask() {
      this.tasks.push({ name: this.task, id: counter });
      counter++;
      this.task = "";
    }, 
    deleteTask(id) {
      this.tasks.splice(this.tasks.findIndex(task => task.id === id), 1)
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";

.holder {
  background: #fff;
}

ul {
  margin: 0;
  padding: 0;
  list-style-type: none;
}

ul li {
  padding: 20px;
  font-size: 1.3em;
  background-color: #e0edf4;
  border-left: 5px solid #3eb3f6;
  margin-bottom: 2px;
  color: #3e5252;
}

p {
  text-align: center;
  padding: 30px 0;
  color: gray;
}

.container {
  box-shadow: 0px 0px 40px lightgray;
}

input {
  width: calc(100% - 40px);
  border: 0;
  padding: 20px;
  font-size: 1.3em;
  background-color: #323333;
  color: #687f7f;
}

.alert {
  background-color: yellow;
  width: 100%;
  height: 30px;
}

.deleteBtn {
  background-color: red;
  height: 30px;
  width: 100px;
  float: right;
  text-align: center center;
  color: white;
  box-shadow: none;
  border: none;
  outline: none;
}
</style>
