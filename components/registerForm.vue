<template>
  <v-sheet id="contact" color="#333333" dark tag="section" tile>
    <div class="py-12"></div>

    <v-container>
      <h2 class="display-2 font-weight-bold mb-3 text-uppercase text-center">Register New User Form</h2>

      <v-responsive class="mx-auto mb-12" width="56">
        <v-divider class="mb-1"></v-divider>

        <v-divider></v-divider>
      </v-responsive>

      <v-theme-provider light>
        <form @submit.prevent="register" ref="form">
          <v-row>

            <v-col cols="12">
              <v-text-field flat v-model="userName" label="Name*" solo></v-text-field>
            </v-col>

            <v-col cols="12">
              <v-text-field flat v-model="password" type="password" label="Password*" solo></v-text-field>
            </v-col>

            <v-col class="mx-auto" cols="auto">
              <v-btn color="accent" x-large @click="register">
                Submit
              </v-btn>
            </v-col>
          </v-row>
        </form>
      </v-theme-provider>
    </v-container>

    <div class="py-12"></div>
  </v-sheet>
</template>

<script>
import alerts from '@/components/alerts.vue'
export default {
  components: {
    alerts
  },
  data() {
    return {
      alertMassge: '',
      success: false,
      userName: '',
      password: '',
    }
  },
  auth: false,
  name: "Register",
  methods: {
    async register() {
      try {
        let data = {
          userName: this.userName,
          password: this.password,
        };
        let response = await this.$axios.post('/api/users/register', data);
        if (response.data.success == true) {
          this.success =true
          this.alertMassge = response.data.message
          this.$auth.loginWith('local', {
            data: {
          userName: this.userName,
          password: this.password,
            }
          }).then(() => {
            this.$router.push('/') 

          }).catch((err) => {
            console.log(err)
          });
        } else if (response.data.success == false){
            this.success = false
            this.alertMassge = response.data.message
        }
      } catch (err) {
        console.log(err);
      }
    },
  }
}

</script>