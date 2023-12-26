

<script>
export default {
  data() {
    return {
      validationStatus: false,
      show2: false,
      email: '',
      newPassword: '',
      confirmPassword: '',
      username: '',
      rules: {
        required: value => !!value || 'Campo obligatorio',
        min: v => v.length >= 8 || 'Mínimo 8 caracteres',
        email: v => /.+@.+\..+/.test(v) || 'Dirección de correo electrónico no válida',
        matchPassword: v => v === this.newPassword || 'Las contraseñas no coinciden',
        requiredUsername: value => !!value || 'Nombre de usuario obligatorio',
      },
    };
  },
  methods: {
    submitForm() {
      if (this.email && this.newPassword && this.newPassword.length >= 8 && this.confirmPassword && this.username) {
        if (this.newPassword !== this.confirmPassword) {
          this.validationStatus = true;
          return;
        }
        this.validationStatus = false;
        this.$router.push("/");
      } else {
        this.validationStatus = true;
      }
    },
  },
};
</script>

<template>
  <v-form>
    <v-container fluid>
      <v-row>
        <v-col
          cols="12"
          class="form_register"
        >
          <img src="logo-olalon.jpg" alt="" class="overlay-img" />
          <v-card-title class="titulo__register">Registrarse</v-card-title>

          <v-card class="form__user__pass">
            <v-text-field
              style="margin: 3%"
              v-model="username"
              :rules="[rules.requiredUsername]"
              label="Nombre de usuario"
            ></v-text-field>

            <v-text-field
              style="margin: 3%"
              v-model="email"
              label="Correo electrónico"
              color="white"
              :rules="[rules.required, rules.email]"
            ></v-text-field>

            <v-text-field
              style="margin: 3%"
              v-model="newPassword"
              :append-icon="show2 ? 'mdi-eye' : 'mdi-eye-off'"
              :rules="[rules.required, rules.min]"
              :type="show2 ? 'text' : 'password'"
              name="input-10-2"
              label="Contraseña"
              hint="Debe tener al menos 8 caracteres"
              counter
              @click:append="show2 = !show2"
            ></v-text-field>

            <v-text-field
              style="margin: 3%"
              v-model="confirmPassword"
              :append-icon="show2 ? 'mdi-eye' : 'mdi-eye-off'"
              :rules="[rules.required, rules.min, rules.matchPassword]"
              :type="show2 ? 'text' : 'password'"
              label="Confirmar contraseña"
            ></v-text-field>

            <div class="button-container">
              <v-btn class="boton__submit" @click="submitForm">Registrarse</v-btn>
              <a href="/" class="login__link">Iniciar sesión</a>
            </div>
            <v-alert
              v-if="validationStatus"
              dense
              outlined
              type="error"
            >
              Correo electrónico o contraseña inválido
            </v-alert>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-form>
</template>

<style scoped>
.form_register {
  left      : 50%;
    top       : 50%;
    position  : absolute;
    transform : translate(-50%, -50%);
    max-width: 35%; 
    float: inline-end;
    background: linear-gradient(rgb(0, 0, 0), rgb(238, 244, 46));
    border-radius: 40px;
    display: flex;
    flex-direction: column;
    place-content: center;
    place-items: center;
  }

.titulo__register {
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

.login__link {
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
