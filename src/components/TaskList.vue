<template>
    <div class="TaskList">
    <table class="table">
        <div v-bind:key="user.id" v-for="user in userList">
        <div v-if="user.username == username">
            <thead>
                <tr>
                    <th class="task1">Task</th>
                    <th>Completed</th>
                    <th>Delete</th>
                </tr>
            </thead>
            <tbody>
                <tr v-bind:key="task.id" v-for="task in tasks">
                    <td v-if="task.userId == user.id"> {{task.title}}</td>
                    <td class = "completed" v-if="task.userId == user.id">
                        <div v-if="task.completed == true">
                            <input type="checkbox" id="checkbox1" name="completed" value="false" checked/>
                        </div>
                        <div v-if="task.completed == false">
                            <input type="checkbox" id="checkbox1" name="completed" value="false"/>
                        </div>
                        </td>
                    <td class = "delete" v-if="task.userId == user.id"><img alt="delete" 
                        src="@/assets/delete.png" 
                        class="delete"
                        @click="$emit('delete-task', task.id)"/></td>
                </tr>
            </tbody>
        </div>
        </div>
    </table>
    </div>
</template>

<script>
import axios   from 'axios'
import auth from "../js/auth"

export default {
    name:'TaskList',
    props:{
        tasks: Array
    },  
    data(){
      return{
          userList:[],
          isLoggedIn: auth.isLoggedIn(),
          username: auth.getUsername(),
      };
  },
  created:function(){
      axios.get('https://jsonplaceholder.typicode.com/users')
        .then(response => this.userList = response.data)
        .catch(error=> console.log(error))
  }
}
</script>

<style scoped lang="scss">
.contactList{
    padding: 1rem
}
.delete{
    width:1rem;
    height: auto;
    cursor: pointer;
}
table{
    border-collapse: collapse;
    margin-top: 2%;
    margin-left: auto;
    margin-right: auto;
    text-align: center;
    border: 2px solid black;
    background-color: #f9f9f9;
    border-color: #1673bd;
}
th{
    border: 1px solid;
    background-color: #2c3e50;
    color: #ffffffa6;
}
</style>