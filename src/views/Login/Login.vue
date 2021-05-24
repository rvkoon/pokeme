<style src="./login.module.scss" lang="scss"></style>

<script>
export default {
  name: "Login",
  data(){ 
    return {
      firstname: "",
      lastname: "",
      email: "",
      password: "",
      confirmPassword: "",
      mode: 'login'
    }
  },
  computed: {
    rules(){
      return {
        required: v => !!v || 'Required field',
        email: value => {
          const pattern = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
          return pattern.test(value) || 'Invalid e-mail.'
        }
      }
    }
  },
  methods: {
    handleSubmit(){
      this.$refs.form.validate()
    },
    switchMode(){
      if(this.mode === "login"){
        return this.mode = 'signup'
      }
      this.mode = 'login'
    }
  }
}
</script>


<template>
  <div class="loginPageContainer">
    <div class="bluryBg"></div>
    <div class="loginPopup">
      <h2 v-if="mode === 'login'">LOGIN</h2>
      <h2 v-else>SIGN UP</h2>
      <v-form @submit.prevent="handleSubmit" ref="form">
        <v-text-field
          outlined
          type="text"
          label="Firstname"
          class="rounded-lg"
          v-model="firstname"
          v-if="mode === 'signup'"
          :rules='[rules.required]'
        ></v-text-field>
        <v-text-field
          outlined
          type="text"
          label="Lastname"
          class="rounded-lg"
          v-model="lastname"
          v-if="mode === 'signup'"
          :rules='[rules.required]'
        ></v-text-field>
        <v-text-field
          outlined
          tpe="email"
          label="Email"
          class="rounded-lg"
          v-model="email"
          :rules='[rules.required, rules.email]'
        ></v-text-field>
        <v-text-field
          outlined
          type="password"
          label="Password"
          class="rounded-lg"
          v-model="password"
          :rules='[rules.required]'
        ></v-text-field>
        <v-text-field
          outlined
          type="password"
          label="Confirm Password"
          class="rounded-lg"
          v-model="confirmPassword"
          v-if="mode === 'signup'"
          :rules='[rules.required]'
        ></v-text-field>
        <v-btn type="submit" depressed class="yellow" v-if="mode === 'login'">
          Connect
        </v-btn>
        <v-btn type="submit" depressed class="yellow" v-else>
          Signup
        </v-btn>
      </v-form>
      <p v-if="mode === 'login'">You don't have an account yet ? <span class="switchModeBtn" @click="switchMode">Sign up</span></p>
      <p v-else>You already have an account ? <span class="switchModeBtn" @click="switchMode">Login</span></p>
    </div>
  </div>
</template>