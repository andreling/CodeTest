<template>
  <form @submit.prevent="registerUser">
    <div class="form-group">
      <h2>Register</h2>
      <label for="exampleInputEmail1">Name</label>
      <input type="text" class="form-control" id="name" placeholder="Enter name" v-model="user.name" required />

      <label for="exampleInputEmail1">Username</label>
      <input type="text" class="form-control" id="username" placeholder="Enter username" v-model="user.username" required />
      <small id="emailHelp" class="form-text text-muted">We'll never share your username with anyone else.</small>
    </div>
    <div class="form-group">
      <label for="exampleInputPassword1">Password</label>
      <input type="password" class="form-control" id="password" v-model="user.password" required placeholder="Password"/>
    </div>
    <RouterLink to="/">Already have an account? Login now</RouterLink><br>
    <div v-if="errorMessage" class="error-message">
        {{ errorMessage }}
    </div>
    <div v-if="successMessage" class="success-message">
        {{ successMessage }}
    </div>
    <button type="submit" @click="register()" class="btn btn-primary">Submit</button>
  </form> 
</template>

<script>
  import axios from 'axios';

  export default {
    data() {
      return {
        user: {
          username: '',
          password: '',
          name: '',
        },
        errorMessage:'',
        successMessage:''
      };
    },
    methods: {
      register() {
        axios.post('http://localhost:8080/api/register', this.user)
          .then(response => {
                this.successMessage = 'Registration successful!';
          }).catch(error => {
                this.errorMessage = 'Registration failed';
          });
      }
    }
  };
</script>

<style scoped>
  .register {
    max-width: 400px;
    margin: 0 auto;
  }
  .error-message {
    color: red;
    margin-top: 10px;
  }
  .success-message {
    color: green;
    margin-top: 10px;
  }
</style>