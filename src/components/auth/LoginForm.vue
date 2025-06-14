<template>
  <div class="q-pa-md flex flex-center" style="min-height: 100vh">
    <div style="max-width: 400px; width: 100%">
      <div class="text-h5 text-center q-mb-md">Iniciar Sesión</div>
      <q-form class="q-gutter-md">
        <q-input
          filled
          v-model="email"
          label="Email *"
          type="email"
          hint="Ingresa tu correo electrónico"
          lazy-rules
          :rules="[(val) => !!val || 'Por favor ingresa tu email']"
        />

        <q-input
          filled
          v-model="password"
          label="Password *"
          type="password"
          hint="Ingresa tu contraseña"
          lazy-rules
          :rules="[(val) => !!val || 'Por favor ingresa tu contraseña']"
        />

        <q-toggle v-model="accept" label="Acepto los términos y condiciones" />

        <div class="row items-center q-gutter-sm">
          <q-btn label="Iniciar sesión" @click="iniciarSesion" type="button" color="primary" />
          <q-btn label="Cancelar" type="reset" color="primary" flat />
        </div>
        <div class="q-mt-md">
          <q-btn
            flat
            label="¿No tienes cuenta? Regístrate"
            color="secondary"
            @click="redirigirRegistro"
          />
        </div>
      </q-form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LoginForm',
  data() {
    return {
      email: '',
      password: '',
      accept: false,
    }
  },
  methods: {
    iniciarSesion() {
      // Aquí iría la lógica de autenticación
      if (!this.accept) {
        this.$q.notify({ type: 'negative', message: 'Debes aceptar los términos y condiciones.' })
        return
      }

      let endpointURL = '/api/users/signin'
      let user = {
        email: this.email,
        password: this.password,
      }
      this.$api
        .post(endpointURL, user)
        .then((response) => {
          console.log('Login successful:', response.data)
          localStorage.setItem('token', response.data.token)
          localStorage.setItem('user', JSON.stringify(response.data))
          this.$q.notify({ type: 'positive', message: 'Inicio de sesión exitoso.' })
          // Redirigir o realizar otras acciones después del login
          this.$router.push('/')
        })
        .catch((error) => {
          this.$q.notify({ type: 'negative', message: 'Error al iniciar sesión: ' + error.message })
        })
      // ... lógica real de login ...
    },
    onReset() {
      this.email = ''
      this.password = ''
      this.accept = false
    },
    redirigirRegistro() {
      this.$router.push({ name: 'register' })
    },
  },
}
</script>

<style></style>
