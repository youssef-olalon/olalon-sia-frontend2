<script>
// Exporta un objeto que define el componente
export default {
  // Datos locales del componente
  data() {
    return {
      validationStatus: false, // Estado de validación
      darkmode: false, // Modo oscuro
      show1: false, // Estado para mostrar la contraseña
      password: '', // Campo de contraseña
      username: '', // Campo de usuario
      rules: {
        // Reglas de validación
        required: value => !!value || 'Campo obligatorio',
        min: v => v.length >= 8 || 'Mínimo 8 caracteres',
        emailMatch: () => (`El usuario y la contraseña no son correctos`),
      },
    }
  },

  // Métodos del componente
  methods: {
    // Método para enviar el formulario
    submitForm() {
      if (this.username == "youssef" && this.password == "youssef03") {
        // Si el usuario y contraseña son correctos, cambia el estado de validación y redirige a '/dashboard'
        this.validationStatus = false,
        this.$router.push("/dashboard");
      } else {
        // Si no son correctos, establece el estado de validación como verdadero
        this.validationStatus = true

      }
    },
  },
}
</script>
<template>
  <v-form>
    <v-container fluid>
      <v-row>

        <v-col
          cols="12"
          class="form_login"
        >
        <img src="logo-olalon.jpg" alt="" class="overlay-img" />
        <v-card-title class="titulo__login">
              Iniciar sesíon
        </v-card-title>

          <v-card class="form__user__pass">

            <v-text-field
              style="margin:3%"
              v-model="username"
              label="Usuario"
              color="white"
            ></v-text-field>

            <v-text-field
              style="margin: 3%"
              v-model="password"
              :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
              :rules="[rules.required, rules.min]"
              :type="show1 ? 'text' : 'password'"
              name="input-10-1"
              label="Contraseña"
              hint="tiene que ser de  8 characteres"
              counter
              @click:append="show1 = !show1"
            ></v-text-field>
            <div class="button-container">
              <v-btn class="boton__submit" @click="submitForm">Iniciar sesión</v-btn>
              <a href="./register" class="register__link">Registrarse</a>
            </div>
            <v-alert
              v-if="validationStatus"
              dense
              outlined
              type="error"
            >
              Invalido <strong>usuario</strong> o <strong>la contraseña</strong>
            </v-alert>
          </v-card>

        </v-col>

      </v-row>
    </v-container>
  </v-form>
</template>

<style scoped>
.form_login {
    left      : 50%;
    top       : 50%;
    position  : absolute;
    transform : translate(-50%, -50%);
    max-width: 35%; 
    padding: 60px;
    float: inline-end;
    background: linear-gradient(rgb(0, 0, 0), rgb(238, 244, 46));
    border-radius: 40px;
    display: flex;
    flex-direction: column;
    place-content: center;
    place-items: center;

}
.titulo__login {
display: flex;
place-content: center;
color: white;
}
.form__user__pass{
color: black;
background: transparent;
display: flex;
flex-direction: column; 
gap: 20px;
border-radius: 20px;
width:300px;
}
.boton__submit {
  width: 150px;
  margin-bottom: 10px;
  border-radius: 30px;
}

.register__link {
  text-decoration: none;
  color: rgb(52, 54, 55);
}

.button-container {
  display: flex;
  flex-direction: column;
  align-items: center;
 gap: 20px;
}
.overlay-img{
  width: 100px;
  height: 100px;
  border-radius: 50px;
}



</style>
