<template>
    <div class="addTask">
    <form @submit="addContact">
    
        <label for="task"> Task: </label>
        <input class="text1" type="text" v-model="title" name="title" placeholder="Task"/>

        <label for="checkbox"> Completed: </label>
        <input type="checkbox" v-model="completed" name="completed" value="false"/>
    
        <button class="button"> Add Task </button>

    </form>
    </div>
</template>

<script>

export default {
    name:'AddTask',
    data(){
        return{
            title: '',
            completed: false,
        };
    }, 
    methods:{
        addContact(event){
            // prevent from submiting the page
            event.preventDefault();
            console.log("add contact clicked")
            //collect the data
            const newContact ={
                title: this.title,
                completed: this.completed,
            };
            this.$emit('add-contact', newContact);
            this.title = '';
            this.completed;

            console.log(newContact.title);
            console.log(newContact.completed);
        }
    }
}
</script>

<style scoped lang="scss">
.addContact {
    padding: 1rem;  
}
label[for=task]{
  padding-left: 500px;
  font-weight: bold;
  font-size: 20px;
}
label[for=checkbox]{
  font-weight: bold;
  font-size: 20px;
}
.text1{
    padding-right: 1px;
    padding-block: 0px;
}
.button{
    margin-left: 10px;
    padding-block: 5px;
}
</style>