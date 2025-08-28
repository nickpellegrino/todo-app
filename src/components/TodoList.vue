<template>
  <div class="todo-container">
    <h2>Burlington Store To-Do Checklist</h2>
    <input v-model="newTask" @keyup.enter="addTask" placeholder="Add a new task..." />
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        <span :class="{ completed: task.completed }" @click="toggleTask(index)">
          {{ task.text }}
        </span>
        <button @click="removeTask(index)">X</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: []
    };
  },
// mounted() {
    // Testing an error here...
 //  throw new Error("This is a test error for GTM");
 // },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({ text: this.newTask, completed: false });
        // push to gtm dataLayer
        window.dataLayer = window.dataLayer || [];
        window.dataLayer.push({
        event: 'add_task',
        task_text: this.newTask
    });
        this.newTask = '';
      }
    },
    toggleTask(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    }
  }
};
</script>

<style scoped>
h2 {
  font-size: 2rem;
}
.todo-container {
  max-width: 100%;
  margin: auto;
  text-align: center;
}
.completed {
  text-decoration: line-through;
  color: gray;
}
button {
  margin-left: 10px;
  cursor: pointer;
}
ul {
list-style-type: none;
}
ul li {
  color: #000;
  margin: .5rem 0;
  padding: 0n;
  font-weight: bold;
  text-transform: capitalize;
}
button {
  background: #000;
  color:#FFF;
  border: none;
  padding: .25rem;
  font-size: 1rem;
  font-weight: bold;
  width: 30px;
  border-radius: 5px;
}
input {
  background: #af003d;
  color: #FFF;
  padding: 1rem;
  border-radius: 2rem;
  width: 400px;
  font-weight: bold;
}
::placeholder {
  color: #FFF;
  font-size: 1rem;
  text-align: center;
}
span {
  background: #c0c0c0;
  padding: 0.25rem;
}
</style>
