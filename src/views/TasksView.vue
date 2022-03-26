<template> 
  <div  class="tasks">
    <div v-if="!isLoggedIn" >
        Login to access this page. 
    </div>
    <div v-if="isLoggedIn">
      <TaskList :tasks="taskList" v-on:delete-task="deleteTask"/>
      <AddTask v-on:add-contact="insertContact"/>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import AddTask from '../components/AddTask.vue'
import TaskList from '../components/TaskList.vue'
import axios   from 'axios'
import auth from "../js/auth"

export default {
  name: 'TasksView',
  components: {
    AddTask, TaskList
  },
  data(){
      return{
          taskList:[],
          isLoggedIn: auth.isLoggedIn()
      };
  },
  created:function(){
      axios.get('https://jsonplaceholder.typicode.com/todos')
        .then(response => this.taskList = response.data)
        .catch(error=> console.log(error))
        
  },
  methods: {
      deleteTask(id){
          axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
          .then( () => this.taskList =
            this.taskList.filter(task => task.id !==id))
           .catch(error=> console.log(error))
      },
      insertContact(newContact){
          console.log("insert function called");
          axios.post('https://jsonplaceholder.typicode.com/todos', newContact)
          .then(response => this.taskList = [...this.taskList,response.data] )
          .catch(error=> console.log(error))
      }
  }
}
</script>

<style scoped lang="scss">
</style>