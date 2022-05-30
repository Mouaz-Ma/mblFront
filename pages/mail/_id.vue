<template>
  <v-app id="inspire">
    <v-app-bar app color="white" flat>
      <v-avatar :color="$vuetify.breakpoint.smAndDown ? 'grey darken-1' : 'transparent'" size="32"></v-avatar>

      <v-tabs centered class="ml-n9 mt-5" color="grey darken-1">
        <nuxt-link to="/">
          <v-tab>
            home
          </v-tab>
        </nuxt-link>
        <nuxt-link to="/mail">
          <v-tab>
            inbox
          </v-tab>
        </nuxt-link>
      </v-tabs>

      <v-avatar class="hidden-sm-and-down" color="grey darken-1 shrink" size="32"></v-avatar>
    </v-app-bar>

    <v-main class="grey lighten-3">
      <v-container>
        <v-row>
          <v-col cols="12" sm="2">
            <v-sheet rounded="lg" min-height="268">
              <!--  -->
              {{allMailsData.subject}}
            </v-sheet>
          </v-col>

          <v-col cols="12" sm="8">
            <v-sheet min-height="70vh" rounded="lg">
            {{allMailsData.content}}
              <!--  -->
            </v-sheet>
          </v-col>

          <v-col cols="12" sm="2">
            <v-sheet rounded="lg" min-height="268">
              <!--  -->
            </v-sheet>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
  export default {
    data: () => ({
        allMailsData: ''
    }),
        async asyncData({
      $axios, route
    }) {
      try {
        const allMails = $axios.get('/api/email/'+route.params.id)
        const allMailPromise = await Promise.resolve(allMails)
        const allMailsData = allMailPromise.data.email
        return {
          allMailsData
        }
      } catch (err) {
        console.log(err)
      }
    },
  }
</script>