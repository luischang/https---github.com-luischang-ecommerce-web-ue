<template>
  <div class="q-pa-md flex flex-center" style="min-height: 100vh">
    <div style="max-width: 500px; width: 100%">
      <div class="text-h5 text-center q-mb-md">Registro de Usuario</div>
      <q-form @submit.prevent="registrarUsuario" @reset="onReset" class="q-gutter-md">
        <q-input
          filled
          v-model="form.FirstName"
          label="Nombre *"
          :rules="[(val) => !!val || 'Campo requerido']"
        />
        <q-input
          filled
          v-model="form.LastName"
          label="Apellido *"
          :rules="[(val) => !!val || 'Campo requerido']"
        />
        <q-input
          filled
          v-model="form.Email"
          label="Email *"
          type="email"
          :rules="[(val) => !!val || 'Campo requerido']"
        />
        <q-input
          filled
          v-model="form.Country"
          label="País *"
          :rules="[(val) => !!val || 'Campo requerido']"
        />
        <q-input
          filled
          v-model="form.Address"
          label="Dirección *"
          :rules="[(val) => !!val || 'Campo requerido']"
        />
        <q-input
          filled
          v-model="form.Password"
          label="Contraseña *"
          type="password"
          :rules="[(val) => !!val || 'Campo requerido']"
        />
        <q-input
          filled
          v-model="repeatPassword"
          label="Repetir Contraseña *"
          type="password"
          :rules="[(val) => val === form.Password || 'Las contraseñas no coinciden']"
        />
        <div class="row items-center q-gutter-sm">
          <q-btn label="Registrarse" type="submit" color="primary" />
          <q-btn label="Cancelar" type="reset" color="primary" flat />
        </div>
      </q-form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RegisterForm',
  data() {
    return {
      form: {
        FirstName: '',
        LastName: '',
        Email: '',
        Country: '',
        Address: '',
        Password: '',
        Type: 'U',
      },
      repeatPassword: '',
    }
  },
  methods: {
    registrarUsuario() {
      if (this.form.Password !== this.repeatPassword) {
        this.$q.notify({ type: 'negative', message: 'Las contraseñas no coinciden.' })
        return
      }
      try {
        this.$api
          .post('api/users', this.form)
          .then((response) => {
            console.log('Usuario registrado:', response.data)
            this.$router.push('/login')
          })
          .catch((error) => {
            console.error('Error al registrar usuario:', error)
            this.$q.notify({ type: 'negative', message: 'Error al registrar usuario.' })
          })
      } catch (e) {
        console.error('Error al registrar usuario:', e)
        this.$q.notify({ type: 'negative', message: 'Error al registrar usuario.' })
      }
    },
    onReset() {
      this.form = {
        FirstName: '',
        LastName: '',
        Email: '',
        Country: '',
        Address: '',
        Password: '',
        Type: 'U',
      }
      this.repeatPassword = ''
    },
  },
}
</script>

<style></style>
