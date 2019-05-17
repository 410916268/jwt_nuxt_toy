<template>
  <div class="container">
    <h1>Sign in to access the secret page</h1>
    <div>
      <label>
        <input  v-model="username">
      </label>
      <label>
        <input type="password" v-model="password">
      </label>
      <button @click="postLogin">
        login
      </button>
    </div>
  </div>
</template>

<script>
const Cookie = process.client ? require('js-cookie') : undefined
import axios from 'axios'
export default {
  middleware: 'notAuthenticated',
  data(){
    return{
      username:'',
      password:'',
    }
  },
  methods: {
    postLogin(){
      self = this
      axios.post('http://127.0.0.1:5000/login',{
        username: this.username,
        password: this.password
      }).then(function (response) {
        if(response.status == 200){
          const auth = 'Bearer '+response.data.access_token
          self.$store.commit('setAuth',auth)
          Cookie.set('auth', auth)
          self.$router.push('/')
        }
      }).catch(function (error) {
        console.log(error);
      });
    }
  }
}
</script>