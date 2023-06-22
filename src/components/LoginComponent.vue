<template>
  <div>
    <b-container fluid>
      <b-row>
        <b-col></b-col>
        <b-col>
          <!-- Inicio de Sesión -->
          <b-form v-if="show" @submit="onSubmit" @reset="onReset" class="login-form">
            <img class="img-login" src="../assets/images/LogoLogin.png" alt="">
            <b-form-group id="input-group-1" label="Usuario" label-for="input-1" :invalid-feedback="usuarioValidationMessage" :state="isUsuarioValid">
              <b-form-input
                id="input-1"
                v-model="form.usuario"
                type="text"
                placeholder="Tu usuario"
                required
              ></b-form-input>
            </b-form-group>

            <b-form-group id="input-group-2" label="Contraseña" label-for="input-2" :invalid-feedback="contraseñaValidationMessage" :state="isContraseñaValid">
              <b-form-input
                id="input-2"
                v-model="form.contraseña"
                placeholder="Tu contraseña"
                type="password"
                required
              ></b-form-input>
            </b-form-group>

            <b-form-group id="select-group-3">
              <p>
                Si aún no estás registrado... Regístrate
                <a href="#" v-on:click="changeForm">ahora</a>
              </p>
            </b-form-group>

            <b-button type="submit" variant="primary">Ingresar</b-button>
            <b-button type="reset" variant="danger">Regresar</b-button>

            <div>
              <h4>Ingresa con tu usuario para comprar o realizar consultas</h4>
            </div>
          </b-form>

          <!-- Formulario de Registro -->
          <b-form v-else @submit="onSubmit" @reset="onReset" class="login-form">
            <img class="img-login" src="../assets/images/LogoLogin.png" alt="">
            <b-form-group id="input-group-1" label="Nombre de Usuario" label-for="input-1" :invalid-feedback="usuarioValidationMessage" :state="isUsuarioValid">
              <b-form-input
                id="input-1"
                v-model="form.usuario"
                type="text"
                placeholder="Tu usuario para ingresar"
                required
              ></b-form-input>
            </b-form-group>

            <b-form-group id="input-group-3" label="Nombre" label-for="input-3" :invalid-feedback="nombreValidationMessage" :state="isNombreValid">
              <b-form-input
                id="input-3"
                v-model="form.nombre"
                type="text"
                placeholder="Tu nombre"
                required
              ></b-form-input>
            </b-form-group>

            <b-form-group id="input-group-4" label="Apellido" label-for="input-4" :invalid-feedback="apellidoValidationMessage" :state="isApellidoValid">
              <b-form-input
                id="input-4"
                v-model="form.apellido"
                type="text"
                placeholder="Tu apellido"
                required
              ></b-form-input>
            </b-form-group>

            <b-form-group id="input-group-5" label="Contraseña" label-for="input-5" :invalid-feedback="contraseñaValidationMessage" :state="isContraseñaValid">
              <b-form-input
                id="input-5"
                v-model="form.contraseña"
                placeholder="Ingresar contraseña"
                type="password"
                required
              ></b-form-input>
            </b-form-group>

            <b-form-group id="input-group-2" label="Email" label-for="input-2" :invalid-feedback="emailValidationMessage" :state="isEmailValid">
              <b-form-input
                id="input-2"
                v-model="form.email"
                type="email"
                placeholder="Email de registro"
                required
              ></b-form-input>
              <!-- Input para recibir notificaciones-->
              <div>
                <input class="form-check-input" type="checkbox" name="" id="checkbox1" v-model="notificacion">
                <label class="form-check-label" for="checkbox1"> Recibir noticias y novedades</label>
              </div>
            </b-form-group>

            <b-form-group id="input-group-6" label="Teléfono" label-for="input-6" :invalid-feedback="telefonoValidationMessage" :state="isTelefonoValid">
              <b-form-input
                id="input-6"
                v-model="form.telefono"
                type="number"
                placeholder="Teléfono sin el 0 y sin el 15"
                required
              ></b-form-input>
            </b-form-group>

            <b-form-group id="select-group-3">
              <p>
                ¿Ya tienes una cuenta? Ingresa
                <a href="#" v-on:click="changeForm">aquí.</a>
              </p>
            </b-form-group>

            <b-form-group>
              <input class="form-check-input" type="checkbox" name="" id="checkbox2" v-model="Bases" required>
              <label class="form-check-label" for="checkbox2"> Acepto términos y condiciones</label>
            </b-form-group>

            <b-button type="submit" variant="primary">Ingresar</b-button>
            <b-button type="reset" variant="danger">Regresar</b-button>
          </b-form>
        </b-col>
        <b-col></b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  name: "LoginComponent",
  data() {
    return {
      form: {
        nombre: "",
        apellido: "",
        email: "",
        contraseña: "",
        telefono: "",
        usuario: "",
        notificacion: "",
        Bases: "",
      },
      show: true,
    };
  },
  computed: {
    isUsuarioValid() {
      return this.form.usuario.length >= 6;
    },
    usuarioValidationMessage() {
      return this.isUsuarioValid ? "" : "El usuario debe tener al menos 6 caracteres.";
    },
    isContraseñaValid() {
      return this.form.contraseña.length >= 8;
    },
    contraseñaValidationMessage() {
      return this.isContraseñaValid ? "" : "La contraseña debe tener al menos 8 caracteres.";
    },
    isNombreValid() {
      return this.form.nombre.length > 0;
    },
    nombreValidationMessage() {
      return this.isNombreValid ? "" : "Ingresa tu nombre.";
    },
    isApellidoValid() {
      return this.form.apellido.length > 0;
    },
    apellidoValidationMessage() {
      return this.isApellidoValid ? "" : "Ingresa tu apellido.";
    },
    isEmailValid() {
      return this.validateEmail(this.form.email);
    },
    emailValidationMessage() {
      return this.isEmailValid ? "" : "Ingresa un email válido.";
    },
    isTelefonoValid() {
      return this.validateTelefono(this.form.telefono);
    },
    telefonoValidationMessage() {
      return this.isTelefonoValid ? "" : "Ingresa un número de teléfono válido.";
    },
  },
  methods: {
    onSubmit(event) {
      event.preventDefault();
      console.log("usuario a loguear: ", JSON.stringify(this.form));
      this.$emit("logged", false);
    },
    onReset(event) {
      event.preventDefault();

      // Resetear valores 
      this.form.usuario = "";
      this.form.nombre = "";
      this.form.apellido = "";
      this.form.email = "";
      this.form.contraseña = "";
      this.form.telefono = "";
      this.form.notificacion = "";
      this.form.Bases = "";

      // restablecer/borrar el estado de validación del formulario
      this.show = false;
      this.$nextTick(() => {
        this.show = true;
      });
    },
    changeForm() {
      this.show = !this.show;
    },
    validateEmail(email) {
      // Simple email validation regex
      const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      return regex.test(email);
    },
    validateTelefono(telefono) {
      // Simple phone number validation regex
      const regex = /^[0-9]{8}$/;
      return regex.test(telefono);
    },
  },
};
</script>

<style scoped>
.cabecera {
  height: 80px;
}

.img-login {
  max-height: 100px;
  max-width: 100px;
  margin-bottom: 30px;
}

.login-form {
  color: rgb(66, 60, 68);
  margin-top: 130px;
  margin-bottom: 70px;
}

button {
  margin-right: 1rem;
  margin-left: 1rem;
  margin-top: 1rem;
  margin-bottom: 1rem;
}
</style>

