<template>

  <v-sheet id="contact" color="#333333" dark tag="section" tile>
    <div class="py-12"></div>
    <!-- alerts -->
    <!-- <div v-if="alertMassge">
      <alerts :message=alertMassge :success=success />
    </div> -->
    <v-container>
      <h2 class="display-2 font-weight-bold mb-3 text-uppercase text-center">Login Form</h2>

      <v-responsive class="mx-auto mb-12" width="56">
        <v-divider class="mb-1"></v-divider>

        <v-divider></v-divider>
      </v-responsive>

      <v-theme-provider light>
        <form @submit.prevent="signIn" ref="form">
          <v-row>

            <v-col cols="12">
              <v-text-field flat v-model="userName" label="Name*" solo></v-text-field>
            </v-col>

            <v-col cols="12">
              <v-text-field flat v-model="password" type="password" label="Password*" solo></v-text-field>
            </v-col>

            <v-col class="mx-auto" cols="auto">
              <v-btn color="accent" x-large @click="signIn">
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
      auth: false,
      name: 'login',
  data() {
    return {
      alertMassge: '',
      success: false,
      userName: '',
      password: '',
    }
  },
methods:{
    async signIn() {
      try {
        let response = await this.$auth.loginWith('local', {
          data: {
            userName: this.userName,
            password: this.password,
          }
        }).then(() => { this.$router.push( {path : '/'}) }, 3000);
        console.log(response)
        if (response.data.success === true) {
          this.success = true
          this.$router.push('/')
        } else {
          this.success = false
        }
      } catch (err) {
        this.success = false
        this.alertMassge = "somthing went wrong"
        console.log(err);
      }
    }
}
}
</script>