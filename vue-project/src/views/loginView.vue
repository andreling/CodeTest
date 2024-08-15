<template>
  <form @submit.prevent="registerUser">
    <div class="form-group">
      <h2>Login</h2>
      <label for="exampleInputEmail1">Username</label>
      <input type="text" class="form-control" id="username" aria-describedby="emailHelp" placeholder="Enter username" v-model="user.username" required />
      <small id="emailHelp" class="form-text text-muted">We'll never share your username with anyone else.</small>
    </div>
    <div class="form-group">
      <label for="exampleInputPassword1">Password</label>
      <input type="password" class="form-control" id="password" v-model="user.password" required placeholder="Password"/>
    </div>
    <RouterLink to="/register">Dont have an account? Register now</RouterLink> <br>
    <div v-if="errorMessage" class="error-message">
      {{ errorMessage }}
    </div>

    <div v-if="successMessage" class="success-message">
      {{ successMessage }}
    </div>
    <button type="submit" @click="login()" class="btn btn-primary">Submit</button>
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
        successMessage:'',
        fetchedData: null
      };
    },
    methods: {
      login() {
        axios.post('http://localhost:8080/api/login', this.user)
          .then(response => {
              this.$router.push({ name: 'home', params: { name: response.data}})
          }).catch(error => {
                this.errorMessage = 'Login failed';
          });
      }
    }
  };
</script>

<style scoped>
  .error-message {
    color: red;
    margin-top: 10px;
  }
  .success-message {
    color: green;
    margin-top: 10px;
  }
</style>