<template>
  <v-container fluid>
    <v-layout row wrap>
      <v-flex xs12>
        <v-item-group>
          <v-form ref="form" v-model="valid" lazy-validation>
            <v-text-field v-model="email" :rules="emailRules" label="E-mail" required></v-text-field>

            <v-text-field
              v-model="password"
              :append-icon="showPassword ? 'fa-eye' : 'fa-eye-slash'"
              :rules="passwordRules"
              :type="showPassword ? 'text' : 'password'"
              name="password"
              label="Password"
              hint="At least 4 characters"
              required
              @click:append="showPassword = !showPassword"
            ></v-text-field>

            <v-btn :disabled="!valid" color="primary" @click="validate">Sign In</v-btn>
          </v-form>

          <v-layout class="justify-center" row wrap>
            <v-flex class="text-xs-center" mt-5>
              <div v-if="errors.length">
                <v-list>
                  <v-alert
                    :value="true"
                    type="error"
                    class="error v-alert"
                    :key="error.text"
                    icon="warning"
                    v-for="error in errors"
                  >{{ error }}</v-alert>
                </v-list>
              </div>
            </v-flex>
          </v-layout>
        </v-item-group>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    valid: true,
    showPassword: false,
    email: "test@test.com",
    submitted: false,
    loading: false,
    returnUrl: "",
    errors: [],
    emailRules: [
      v => !!v || "E-mail is required",
      v => /.+@.+/.test(v) || "E-mail must be valid"
    ],
    password: "",
    passwordRules: [
      v => !!v || "Password is required",
      v => (v && v.length >= 4) || "Password must be at least 4 characters long"
    ]
  }),
  created() {
    // get return url from route parameters or default to '/'
    this.returnUrl = this.$route.query.returnUrl || "/";
  },
  methods: {
    validate() {
      if (this.$refs.form.validate()) {
        console.log("javascript verification valid");

        this.loading = true;
      }
    },
    reset() {
      this.$refs.form.reset();
    },
    resetValidation() {
      this.$refs.form.resetValidation();
    }
  }
};
</script>
