<template>
  <v-card class="mx-auto" max-width="400">
    <v-container fluid>
      <v-row dense justify="center" align="center">
        <v-col>
          <v-form ref="form" v-model="valid" lazy-validation>
            <v-text-field
              v-model="email"
              :rules="emailRules"
              label="E-mail"
              required
            ></v-text-field>

            <v-text-field
              v-model="password"
              :append-icon="show ? 'mdi-eye' : 'mdi-eye-off'"
              :rules="passwordRules"
              :type="show ? 'text' : 'password'"
              label="Пароль"
              required
              @click:append="show = !show"
            ></v-text-field>

            <v-btn
              :disabled="!valid"
              color="success"
              class="mr-4"
              @click="login"
            >
              Войти
            </v-btn>
          </v-form>
        </v-col>
      </v-row>
    </v-container>
  </v-card>
</template>

<script>
export default {
  data: function data() {
    return {
      valid: false,
      show: false,
      email: '',
      emailRules: [
        (v) => !!v || 'Введите Email',
        (v) => /.+@.+\..+/.test(v) || 'Некорректный Email',
      ],
      password: '',
      passwordRules: [
        (v) => !!v || 'Введите пароль',
        (v) => (v && v.length >= 6) || 'Пароль слишком короткий',
      ],
    }
  },

  methods: {
    login: async function () {
			try {
				const response = await this.$auth.loginWith('local', {
          data: {
						email: this.email,
						password: this.password
					}
        })
			} catch (error) {
				alert(error)
			}
		},
  },
}
</script>