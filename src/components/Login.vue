<template>
  <div class="flex rounded-md shadow-lg">
    <div class="m-auto p-8 bg-white shadow-md rounded-md">
      <div class="text-center mb-6">
        <img src="wordpress.png" alt="WordPress Logo" class="w-16 h-16 mx-auto mb-2" />
      </div>


      <form v-if="loginType === 'password'">
        <p class="my-3">Username or Email Address</p>
        <div class="mb-4">
          <input v-model="emailOrUsername" type="text" class="w-full p-1 border rounded" placeholder="Email or Username" />
        </div>
        <p class="mb-3">Password</p>
        <div class="mb-4">
          <input v-model="password" type="password" class="w-full p-1 border rounded" placeholder="Password" />
        </div>
        <div class="flex items-center justify-between m-2">
          <input type="checkbox" class="mr-1" />
          <label class="text-md mr-8">Remember me</label>
          <button @click.prevent="login" class="w-1/4 px-3 py-2 ml-6 bg-blue-500 text-white rounded hover:bg-blue-600">
           Login
          </button>
        </div>
      </form>


      <form v-else-if="loginType === 'magic-link'">
        <div class="mb-4">
          <p class="mb-2">Email or Phone</p>
          <input v-model="magicLinkEmail" type="email" class="w-full p-1 border rounded" placeholder="Enter Email or Phone" />
        </div>
        <button class="w-full px-3 py-2 bg-blue-500 text-white rounded hover:bg-blue-600">
          Send Magic Link
        </button>
        <div class="mt-4">
          <a href="#" class="text-blue-500 mr-4 custom-underline " @click.prevent="switchToPasswordLogin">Login with password</a> 
          <a href="#" class="text-blue-500 custom-underline" @click.prevent="switchToOTPLink">Login with OTP</a>
          
        </div>
      </form>

      
 
      <form v-else-if="loginType === 'otp'">
        <div class="mb-4">
          <p>Email or Phone </p>
          <input v-model="otpEmailOrPhone" type="text" class="w-full p-1 border rounded" placeholder="Enter Email or Phone" />
        </div>
        <button class="w-full px-3 py-2 bg-blue-500 text-white rounded hover:bg-blue-600">
          Send OTP
        </button>
        <div class="mt-4">
          <a href="#" class="text-blue-500 mr-4 custom-underline" @click.prevent="switchToPasswordLogin">Login with password</a> 
          <a href="#" class="text-blue-500 custom-underline" @click.prevent="switchToMagicLinkLogin">Login with magic link</a>
          
        </div>
      </form>


      <div class="mt-4">
        <a v-if="loginType === 'password'" href="#" class="text-blue-500 mr-6 custom-underline" @click.prevent="toggleMagicLinkForm">Login with magic link</a>
        <a v-if="loginType === 'password'" href="#" class="text-blue-500 custom-underline" @click.prevent="switchToOTPLink">Login with OTP</a>
      </div>
      <div class="mt-4">
        <a v-if="loginType === 'password'" href="#" class="text-black">Load your password?</a>
      </div>
      <div class="mt-4">
        <a href="https://wordpress.com" target="_blank" class="text-black"> Go to my WordPress site</a>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const loginType = ref('password');
const emailOrUsername = ref(localStorage.getItem('emailOrUsername') || ''); // Load from localStorage
const password = ref(localStorage.getItem('password') || ''); // Load from localStorage
const magicLinkEmail = ref('');
const otpEmailOrPhone = ref('');

function login() {
  // login logic 
  console.log('Logging in...');
}

function toggleMagicLinkForm() {
  loginType.value = loginType.value === 'magic-link' ? 'password' : 'magic-link';
}

function switchToPasswordLogin() {
  loginType.value = 'password';
}

function switchToMagicLinkLogin() {
  loginType.value = 'magic-link';
}
function switchToOTPLink() {
  loginType.value = 'otp';
}

// Save email and password to localStorage whenever they change
function saveCredentials() {
  localStorage.setItem('emailOrUsername', emailOrUsername.value);
  localStorage.setItem('password', password.value);
}

// Save email and password initially after component is mounted
onMounted(() => {
  saveCredentials();
});
</script>

<style>

</style>
