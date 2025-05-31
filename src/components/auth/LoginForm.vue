<template>
  <h1>Hola Mundo, soy Login</h1>
  <input v-model="email" type="text" placeholder="Email" required />
  <input v-model="password" type="password" placeholder="Password" required />

  <button @click="validate">Login</button>
</template>

<script>
export default {
  name: 'LoginForm',
  data() {
    return {
      email: '',
      password: '',
    }
  },
  methods: {
    validate() {
      console.log('Click del botón....... Email: ' + this.email)
    },
  },
}
</script>

<style></style>
