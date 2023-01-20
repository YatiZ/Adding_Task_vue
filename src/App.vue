<template>
  <div class="container">
    <Header @toggle-add-task="toggleAddTask" title="Important Events" :showAddTask = "showAddTask" />
    <div v-show="showAddTask">
      <AddTask @add-task="addTask"/>
    </div>
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks"/>
  </div>
  
</template>

<script>
import AddTask from './components/AddTask'
import Header from './components/Header'
import Tasks from './components/Tasks.vue'
export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask
  },
  data(){
    return{
      tasks:[],
      showAddTask:false
    }
  },
  methods:{
    toggleAddTask(){
      this.showAddTask =! this.showAddTask
    },
    addTask(task){
      this.tasks = [...this.tasks,task]
    },
   deleteTask(id){
    if(confirm('Are you sure?')){
      this.tasks = this.tasks.filter((task)=>task.id !== id)
    }
    
   },
    toggleReminder(id){
      this.tasks = this.tasks.map((task)=>task.id === id? { ...task,reminder: !task.reminder} : task)
    }
  },
  created(){
    this.tasks = [ 
      {
        id:1,
        text:'Doctors Appointment',
        day:'March 1st at 2:30PM',
        reminder:true,
      },
      {
        id:2,
        text:'Meeting at School',
        day:'March 3rd at 1:30pm',
        reminder: false,
      },
      {
        id:3,
        text:'Date with him',
        day:'March 4th at 2:30PM',
        reminder:true,
      },
      {
        id:4,
        text:'Family Reunion',
        day:'March 23rd at 4:30pm',
        reminder:true,
      }
    ]
  }
}
</script>


<style>
  @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;1,900&display=swap');
  .container{
    max-width: 500px;
    margin: 30px auto;
    overflow: auto;
    min-height: 300px;
    border: 1px solid steelblue;
    padding: 30px;
    border-radius: 5px;
  }
  .btn{
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
  .btn:focus{
    outline: none;
  }
</style>

