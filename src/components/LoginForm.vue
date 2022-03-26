<template>
    <form class="label" @submit.prevent="login">
        <label for="username"> Username: </label>
        <input type="text" v-model="username" name="username" placeholder="Username"/>
        <p></p>
        <label for="password"> Password: </label>
        <input type="password" v-model="password" name="password" placeholder="Password"/>
        <div v-if="errorMessage"> {{errorMessage}} </div>
        <p></p>
        <button class="btn"> Login </button>
    </form>
</template>

  
<script>
    import auth from '../js/auth';
    export default {
        name: "LoginForm",
        data(){
            return{
                username: "Bret",
                password: "hildegard.org",
                errorMessage: "",
            }
        },
        methods:{
            login(){
                console.log('Call login()');
                auth.login(this.username, this.password, (res) => {
                    if (res.auth){
                        //Login succesful, go to home page.
                        console.log('Loggin success');
                        this.$router.replace('/');
                    } else{
                        //Login failed.
                        console.log('Loggin failed');
                        this.errorMessage = "Loggin failed";
                    }
                })
            },
        }
    }
</script>

<style lang="scss">
.label{
    margin-top: 5%;

}
label[for=username]{
  padding: 100px;
  margin: 10px;
  font-weight: bold;
  font-size: 20px;
}
input[type=text] {
  padding-right: 400px;
  padding-block: 0px;
  margin: 10px;
  font-size: 20px;
}
label[for=password]{
  padding: 100px;
  margin: 10px;
  font-weight: bold;
  font-size: 20px;
}
input[type=password] {
  padding-right: 400px;
  padding-block: 0px;
  margin: 10px;
  font-size: 20px;
}
.btn{
  padding: 0px 310px;
  margin-left: 336px;
  text-align: center;
  font-size: 15px;
}
</style>
