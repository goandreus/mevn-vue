<template>
  <div class="container">
    <h1>Login</h1>
    <form @submit.prevent="login">
      <input type="email" placeholder="Email" class="form-control my-2" v-model="usuario.email">
      <input type="text" placeholder="Contraseña" class="form-control my-2" v-model="usuario.pass">
      <b-button class="btn-block" type="submit">Acceder</b-button>
    </form>
    <div v-if="mensaje != ''">
      <p>{{mensaje}}</p>
    </div>
  </div>
</template>

<script>
import { mapActions } from "vuex";

export default {
  data() {
    return {
      usuario: {email: 'usuario3@usuario.com', pass: '123123'},
      mensaje: ''
    }
  },
  methods:{
    ...mapActions(['guardarUsuario']),
    login(){
      // console.log(this.usuario);
      this.axios.post('/login', this.usuario)
        .then(res => {
          console.log(res.data);
          const token = res.data.token;
          this.guardarUsuario(token);
        })
        .catch(e => {
          console.log(e.response);
          this.mensaje = e.response.data.mensaje
        })
    }
  }
}
</script>