<template>
    <div class="header">  
        <router-link style="text-decoration: none; color: inherit;" to="/"> Home </router-link> |
        <router-link style="text-decoration: none; color: inherit;" to="contacts"> Tasks </router-link> |
        <router-link style="text-decoration: none; color: inherit;" v-if="!isLoggedIn" to="login"> Login </router-link>
        <a  v-if="isLoggedIn" v-on:click="logout"> Logout </a>
    </div>
</template>

<script>
    import auth from '../js/auth'
    export default{
        name: 'AppNav',
        data() {
            return { isLoggedIn: auth.isLoggedIn()};
        },
        created(){
            auth.onLoginStatus = isLoggedIn =>{
                this.isLoggedIn = isLoggedIn;
            }
        },
        methods:{
            logout: function(){
                auth.logout( (res) =>{
                    console.log(res)
                });
            }
        }
    }
</script>

<style lang="scss">
.header {
  background-color: #18a1db;
  font-size: 125%;
  color: black;
  word-spacing: 20px;
  line-height: 60px;
}

</style>


