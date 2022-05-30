<template>
  <v-app-bar app color="white" height="100">
    <nuxt-link to="/">
      <v-avatar class="mr-3" color="grey lighten-5" size="70">
        <v-img contain max-height="70%" src="https://mblhightech.com/assets/images/logo/logo-dark.png"></v-img>
      </v-avatar>
    </nuxt-link>

    <v-toolbar-title class="font-weight-black headline">
      MBL Assignment
    </v-toolbar-title>
    <v-spacer></v-spacer>

    <div v-if="$auth.$state.user">
        
      <nuxt-link to="/mail" class="mr-5" v-if="$auth.$state.user.userName === 'jim'">
       <v-badge :content=allMailsData v-if="allMailsData != 0" color="error" bordered>
        <v-btn color="primary" elevation="2">
         Mail Box
        </v-btn>
        </v-badge>
               <v-badge v-else color="green" bordered>
        <v-btn color="primary" elevation="2">
         Mail Box
        </v-btn>
        </v-badge>
      </nuxt-link>
          <nuxt-link v-else to="/mail" class="mr-5">
               <v-badge color="green" bordered>
        <v-btn color="primary" elevation="2">
         Mail Box
        </v-btn>
        </v-badge>
      </nuxt-link>

      <v-btn color="gray" elevation="2" @click="logout()">Log Out</v-btn>
    </div>
    <div v-else>
      <nuxt-link to="/register">
        <v-btn color="primary" elevation="2">Register</v-btn>
      </nuxt-link>

      <nuxt-link to="/login">
        <v-btn class="ml-5" color="gray" elevation="2">Login</v-btn>
      </nuxt-link>
    </div>


  </v-app-bar>
</template>

<script>
export default {
    props: ['allMailsData'],
      methods: {
            async logout() {
                console.log('clicked')
          await this.$auth.logout()
        },
  }
}
</script>