<template>
  <div class="container">
    <h1>Sign up to access the system</h1>
    <div>
      <input  v-model="username">
      <input type="password" v-model="password">
      <button @click="postSignup">
        signup
      </button>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
    data() {
        return {
            username: "",
            password: ""
        }
    },
    methods:{
        postSignup(){
          axios.post('http://127.0.0.1:5000/signup', {
                username: this.username,
                password: this.password
            }).then(function (response) {
                if(response.status == 200){
                  window.location.href = '/login'
                }
            }).catch(function (error) {
                console.log(error);
            });

        }
    }
}
</script>
