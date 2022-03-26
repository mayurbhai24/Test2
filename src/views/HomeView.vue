<template> 
  <div class="home">    
    <div v-if="!isLoggedIn" >
        Login to access this page. 
    </div>
    <div v-if="isLoggedIn">
      <div v-bind:key="profile.id" v-for="profile in profileList">
        <div v-if="profile.username == username">
          <h1 class="head"> Welcome {{profile.name}}</h1>
          <p>Your username is <span class="bold">{{profile.username}}</span></p>
          <p> <span class="bold">Contact Info:</span>
              <ul style="list-style-type:none;">
                <li><span class="bold">E-mail:</span> {{profile.email}}</li>
                <li><span class="bold">Phone:</span> {{profile.phone}}</li>
                <li><span class="bold">Website:</span> {{profile.website}}</li>
                <li><span class="bold">Company:</span> {{profile.company.name}}</li>
                <li><span class="bold">Adress:</span> </li>
                  <ul style="list-style-type:none;">
                    <li><span class="bold">Street:</span> {{profile.address.street}}</li>
                    <li><span class="bold">Suite:</span> {{profile.address.suite}}</li>
                    <li><span class="bold">City:</span> {{profile.address.city}}</li>
                    <li><span class="bold">Zipcode:</span> {{profile.address.zipcode}}</li>
                  </ul>
              </ul>  
          </p>
          <p>Your catch phrase is <span class="bold">{{profile.company.catchPhrase}}</span></p>

        </div>
      </div>
    </div>
    
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'
import axios   from 'axios'
import auth from "../js/auth"

export default {
  name: 'HomeView',
  data(){
    return{
      profileList:[],
      isLoggedIn: auth.isLoggedIn(),
      username: auth.getUsername(),
    };
  },  
  created:function(){
      axios.get('https://jsonplaceholder.typicode.com/users')
        .then(response => this.profileList = response.data)
        .catch(error=> console.log(error))
  },
  
}
</script>

<style scoped lang="scss">
.home{
    margin: 1rem;
}
.head{
  text-align: center;
}
.bold {
  font-weight: bold;
}
p{
  font-size: 20px;
  padding-top: 1%;
}

</style>
