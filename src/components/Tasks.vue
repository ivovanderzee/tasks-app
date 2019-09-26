<template>
  <div class="hello">
    <div class="holder">

<!-- a form which calls the method addTask -->
      <form @submit.prevent="addTask">
        <input type="text" placeholder="Enter a new task" v-model="task" />
      </form>

      <ul>

<!-- the wrapper transition group takes care of the animation when you add a task to your list -->
        <transition-group
          name="list"
          enter-active-class="animated slideInLeft"
          leave-active-class="animated slideOutRight"
        >

<!-- creates a task list item for each task you add to the tasks array in data -->
          <li v-for="task in tasks" v-bind:key="task.id">
            {{ task.name }}
            <button class="deleteBtn" @click="deleteTask(task.id)">delete</button>
          </li>
        </transition-group>
      </ul>

<!-- creates a paragraph that counts the total tasks you added to your list -->
      <p v-if="tasks.length >= 1">You have {{ tasks.length }} tasks to do</p>
      <p v-else>You have nothing to do</p>
    </div>
  </div>
</template>

<script>


let counter = 0;

export default {
  name: "Tasks",

//the data logic of the app. In here the data for the app is defined
  data() {
    return {
      task: "",
      tasks: []
    };
  },



  methods: {


    //a method that pushes the user input to the array tasks. (v-model)
    addTask() {
      this.tasks.push({ name: this.task, id: counter });
      counter++;
      this.task = "";
    }, 

    //a method that can delete a task if the user clicks the delete button
    deleteTask(id) {
      this.tasks.splice(this.tasks.findIndex(task => task.id === id), 1)
    }
  }
};
</script>

<!-- styling that is used in the app -->
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
