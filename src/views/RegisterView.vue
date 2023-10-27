<template>
    <main class="form-signin w-100 m-auto">
      <form @submit.prevent="submit">
        <h1 class="h3 mb-3 fw-normal">Welcome To Registration</h1>
    
        <div class="form-floating">
          <input v-model="data.first_name" class="form-control" id="floatingInput" placeholder="name@example.com">
          <label for="floatingInput">First Name</label>
        </div>
        <div class="form-floating">
          <input v-model="data.last_name" class="form-control" id="floatingInput" placeholder="name@example.com">
          <label for="floatingInput">Last Name</label>
        </div>
        <div class="form-floating">
          <input v-model="data.username" class="form-control" id="floatingInput" placeholder="name@example.com">
          <label for="floatingInput">Username</label>
        </div>
        <div class="form-floating">
          <input v-model="data.email" type="email" class="form-control" id="floatingInput" placeholder="name@example.com">
          <label for="floatingInput">Email address</label>
        </div>
        <div class="form-floating">
          <input v-model="data.password" type="password" class="form-control" id="floatingPassword" placeholder="Password">
          <label for="floatingPassword">Password</label>
        </div>
        <div class="form-floating">
          <input v-model="data.password_confirm" type="password" class="form-control" id="floatingPassword" placeholder="Password">
          <label for="floatingPassword">Repeat Password</label>
        </div>
    
        <button class="btn btn-primary w-100 py-2" type="submit">Sign Up</button>
      </form>
    </main>
    
    </template>
    
    
    <script lang="ts">
    import {reactive} from "vue"
    import axios from 'axios'
    import { useRouter } from "vue-router";
    export default {
        name:"RegisterView",
        setup(){
            const data = reactive({
                'first_name':'',
                'last_name':'',
                'username':'',
                'email':'',
                'password':'',
                'password_confirm':'',
            });
            const router=useRouter();
            const submit=async () => {
                await axios.post('http://localhost:8000/jobs/api/register', data);
                await router.push('/login');
            };

            return{
                data,
                submit,
            }
        }
    }
    </script>
    
    
    <style scoped>
    </style>