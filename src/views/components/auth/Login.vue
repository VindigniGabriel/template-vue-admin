<template>
  <v-container class="fill-height" fluid>
    <v-row align="center" justify="center">
      <v-col cols="12" sm="6">
        <base-material-card>
          <template v-slot:heading>
            <div class="display-2 font-weight-light">Iniciar sesión</div>

            <div class="subtitle-1 font-weight-light">Adminitración Cyber</div>
          </template>

          <v-form ref="form" v-model="valid" lazy-validation class="py-4">
            <v-text-field
              label="Correo"
              class="purple-input"
              prepend-icon="mdi-email"
              :rules="emailRules"
              v-model="email"
              outlined
            />

            <v-text-field
              :append-icon="show ? 'mdi-eye' : 'mdi-eye-off'"
              label="Clave"
              class="purple-input"
              prepend-icon="mdi-incognito"
              :rules="passRules"
              v-model="pass"
              outlined
              :type="show ? 'text' : 'password'"
              @click:append="show = !show"
            />
          </v-form>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="blue darken-1" text @click="login">Ingresar</v-btn>
          </v-card-actions>
        </base-material-card>
      </v-col>
      <Notification />
    </v-row>
  </v-container>
</template>

<script>
import Notification from "../monitor/Notifications";

export default {
  data() {
    return {
      show: false,
      valid: true,
      pass: "secret1234",
      email: "gabriel205414@gmail.com",
      passRules: [v => !!v || "Clave es requerido"],
      emailRules: [
        value => !!value || "Correo es requerido.",
        value => {
          const pattern = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
          return pattern.test(value) || "Correo invalido.";
        }
      ]
    };
  },
  components: {
    Notification
  },
  methods: {
    login() {
      if (this.$refs.form.validate()) {
        let user = {
          email: this.email,
          pass: this.pass
        };
        this.$store.dispatch("SIGN_IN", user);
      } else {
        console.log(this.email, this.pass);
        console.log("Faltan datos");
      }
    }
  }
};
</script>