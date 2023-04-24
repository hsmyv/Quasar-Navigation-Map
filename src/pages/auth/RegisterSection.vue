<template>
  <q-page id="registrationPage">
  <q-toolbar class="text-white bg-teal-8">
      <q-toolbar-title>
        Register
      </q-toolbar-title>
    </q-toolbar>

    <q-scroll-area class="form-style">
      <div class="text-h6 text-center q-pt-md">
        <q-img src="favicon.ico" height="60px" width="60px"/>
        <div>Navigation Map</div>

        <div class="q-pa-md q-gutter-md">
          <div class="text-center">Register and extra features</div>

          <q-input v-model="firstName" outlined stack-label label="First Name">
            <template v-slot:append>
              <q-icon name="close"/>
            </template>
          </q-input>
           <q-input v-model="lastName" outlined stack-label label="Last Name">
            <template v-slot:append>
              <q-icon name="close"/>
            </template>
          </q-input>
           <q-input v-model="email" outlined stack-label label="Email">
            <template v-slot:append>
              <q-icon name="close"/>
            </template>
          </q-input>
           <q-input v-model="password" outlined stack-label label="Password">
            <template v-slot:append>
              <q-icon name="close"/>
            </template>
          </q-input>
           <q-input v-model="confirmPassword" outlined stack-label label="Confirm Password">
            <template v-slot:append>
              <q-icon name="close"/>
            </template>
          </q-input>
          <div>
            <q-btn @click="register" color="black" size="lg" class="full-width" label="Register"/>
          </div>
          <div class="q-px-md q-mt-xl text-center">
            <div class="q-mb-md no-account">Do you have an account?</div>
            <q-btn color="teal" outline rounded to="/auth" size="15px">Login Here</q-btn>
          </div>
        </div>
      </div>
    </q-scroll-area>
  </q-page>
</template>
<script setup>

import { ref } from 'vue'
import { useUserStore } from 'src/stores/user-store'

const userStore = useUserStore()
const firstName = ref('')
const lastName = ref('')
const email = ref('')
const password = ref('')
const confirmPassword = ref('')

const register = async () => {
  await userStore.getSanctumCookie()
  await userStore.register(
    firstName.value,
    lastName.value,
    email.value,
    password.value,
    confirmPassword.value
  )
  const user = await userStore.fetchUser()
  console.log(user)
  userStore.setUser(user.data)
}
</script>
<style lang="scss">
#registrationPage {
    .form-style{
      margin: 0 auto;
      height: calc(100vh - 180px);
      max-width: 500px;
  }
}
</style>
