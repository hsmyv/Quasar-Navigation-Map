<template>
  <q-page id="loginPage">
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
           <q-input  v-model="email" outlined stack-label label="Email">
            <template v-slot:append>
              <q-icon name="close"/>
            </template>
          </q-input>
           <q-input v-model="password" outlined stack-label label="Password">
            <template v-slot:append>
              <q-icon name="close"/>
            </template>
          </q-input>
          <div>
            <q-btn @click="login" color="black" size="lg" class="full-width" label="Login"/>
          </div>

          <div class="q-px-md q-mt-xl text-center">
            <div class="q-mb-md no-account">Don't have an account?</div>
            <q-btn color="teal" outline rounded to="/auth/register" size="15px">Register Here</q-btn>
          </div>
        </div>
      </div>
    </q-scroll-area>
  </q-page>
</template>
<script setup>
import { ref } from 'vue'
import { useUserStore } from '../../stores/user-store'

const userStore = useUserStore()
const email = ref('')
const password = ref('')
const login = async () => {
  await userStore.getSanctumCookie()
  await userStore.login(email.value, password.value)
  const user = await userStore.fetchUser()
  console.log(user)
  userStore.setUser(user.data)
}
</script>
<style lang="scss">
#loginPage {
    .form-style{
      margin: 0 auto;
      height: calc(100vh - 180px);
      max-width: 500px;
  }
  .no-account {
    font-size: 17px;
  }
}
</style>
