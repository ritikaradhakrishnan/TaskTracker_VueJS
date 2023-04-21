<template>
  <div class="container">
    <Header @toggle-add-task="toggleAddTask" 
    title="Task Tracker" 
    :showAddTask="showAddTask"  />
    <div v-show="showAddTask">
      <AddTask @add-task="addTask" />
    </div>
    <!--We pass a dynamic array here and if it changes we have to Tasks.vue so we vbind it tasks to the task data-->
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks"  /> 
  </div>
</template>

<script>
import Header from './components/Header'
import Tasks from './components/Tasks'
import AddTask from './components/AddTask'

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask
  },
  data() { //usually data comes from API, but for now we put data in App.vue and not Task.vue so that every part can access
    return{
      tasks: [],
      showAddTask : false
    }
  },
  methods: {
    toggleAddTask(){
      this.showAddTask = !this.showAddTask //Add Task will show it's placeholders (form)
    },
    addTask(task){
      this.tasks = [...this.tasks, task]
    },
    deleteTask(id) {
      if(confirm('Delete Task?')) { //if(confirm){} in vue to output dialog box
        this.tasks = this.tasks.filter((task) => task.id !== id) //we want every task back except for the task with the id that we pressed 'x' on
      }
    },
    toggleReminder(id){
      this.tasks = this.tasks.map((task) => task.id == id ? {...task, reminder: !task.reminder} : task)
    },
  },
  created() { //life cycle method, typically we would make a request but hard coding for now
    this.tasks = [
      {
        id: 1,
        text: 'Midterm',
        day: 'March 5th',
        reminder: true,
      },
      {
        id: 2,
        text: 'Homework Submission',
        day: 'April 11th',
        reminder: true,
      },{
        id: 3,
        text: 'Birthday',
        day: 'May 20th',
        reminder: false, //now we need a task component to render this data into so that we can load it on the page 
      },
    ]
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>