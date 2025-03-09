<template>
 <div class="min-h-screen flex items-center justify-center bg-gradient-to-t from-cyan-700 to-cyan-50">
  <div class="w-full max-w-md p-8 space-y-6 bg-white shadow-lg rounded-lg">
    <h2 class="text-3xl font-bold text-gray-900 text-center">Sign In to ERP</h2>
    
    <form class="mt-8 space-y-6" @submit.prevent="handleSubmit">
      <div>
        <label for="username" class="block text-sm font-medium text-gray-700">Username</label>
        <input v-model="username" type="text" id="email-address" name="email" required placeholder="Email address" class="form-control" />
      </div>
      <div>
        <label for="password" class="block text-sm font-medium text-gray-700">Password</label>
        <input v-model="password" type="password" id="password" name="password" required placeholder="Password" class="form-control" />
      </div>
      
      <div class="flex justify-between">
        <div class="flex">
          <input type="checkbox" id="remember_me" name="remember_me" class="h-4 w-4 text-cyan-600 focus:ring-cyan-500 border-gray-300 rounded" />
          <label for="remember_me" class="ml-2 block text-sm text-gray-900">Remember me</label>
        </div>

        <div class="TEXT-SM">
          <a href="#" class="font-medium text-cyan-600 hover:text-cyan-500">Forgot your password?</a>
        </div>
      </div>

      <div>
        <button type="submit" class="btn-full">
          Sign In
        </button>
      </div>
    </form>
  </div>
 </div>
</template>

<script setup>
  import axios from 'axios';
  import Swal from 'sweetalert2';
  import config from '@/config';

  const username = ref('');
  const password = ref('');

  const handleSubmit = async () => {
    try {
      //Validate username and password
      if (!username.value || !password.value) {
        Swal.fire({
          icon: 'error',
          title: 'Oops...',
          text: 'Username and Password is required!',
        });
      } else {
        const response = await axios.post(config.apiServer + /api/user/signIn, {
          username: username.value,
          password: password.value,
        });

        //Redirect to dashboard
        if (response.status === 200) {
         console.log(response.data);
        }else{
          Swal.fire({
            icon: 'error',
            title: 'Oops...',
            text: 'Invalid username or password!',
          });
        }
      }
    } catch (error) {
      console.log(error);
    }
  };
</script>
