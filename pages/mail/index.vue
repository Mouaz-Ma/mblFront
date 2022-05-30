<template>
  <v-app id="inspire">
    <v-system-bar app>
      <v-spacer></v-spacer>

          <nuxt-link to="/">
      <v-avatar class="mr-3" color="grey lighten-5" size="70">
       <h1>home</h1>
      </v-avatar>
    </nuxt-link>
    </v-system-bar>

    <v-navigation-drawer
      v-model="drawer"
      app
    >
      <v-sheet
        color="grey lighten-4"
        class="pa-4"
      >
        <v-avatar
          class="mb-4"
          color="grey darken-1"
          size="64"
        ></v-avatar>

        <div>{{$auth.$state.user.userName}}</div>
      </v-sheet>

      <v-divider></v-divider>

      <v-list>
        <v-list-item
          v-for="[icon, text] in links"
          :key="icon"
          link
        >
          <v-list-item-icon>
            <v-icon>{{ icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ text }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-main>
      <v-container
        class="py-8 px-6"
        fluid
      >
        <v-row>
          <v-col
            v-for="card in cards"
            :key="card"
            cols="12"
          >
            <v-card>
              <v-subheader>{{ card }}</v-subheader>

              <v-list two-line>
                <template v-for="mail in allMailsData">
                    <nuxt-link :to="'/mail/'+mail._id">
                  <v-list-item
                  :key="mail.id"
                  >
                    <v-list-item-avatar color="grey darken-1">
                    </v-list-item-avatar>

                    <v-list-item-content>
                        
                      <v-list-item-title v-if="mail.isRead">{{mail.subject}} - not New</v-list-item-title>
                      <v-list-item-title v-else>{{mail.subject}} - New</v-list-item-title>

                      <v-list-item-subtitle>
                        {{mail.content.substring(0, 50)}} ...
                      </v-list-item-subtitle>
                    </v-list-item-content>
                  </v-list-item>
                    </nuxt-link>
                </template>
              </v-list>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
  export default {
    data: () => ({
    allMailsData: [],
      cards: ['Today'],
      drawer: null,
      links: [
        ['mdi-inbox-arrow-down', 'Inbox'],
        ['mdi-send', 'Send'],
        ['mdi-delete', 'Trash'],
        ['mdi-alert-octagon', 'Spam'],
      ],
    }),
            async asyncData({
      $axios,$auth
    }) {
      try {
          if($auth.$state.user.userName === 'jim'){
              const allMails = $axios.get('/api/email/mailList')
              const allMailPromise = await Promise.resolve(allMails)
              const allMailsData = allMailPromise.data.emails
              return {
                allMailsData
              }
          } else {
              allMailsData = []
          }
      } catch (err) {
        console.log(err)
      }
    },
  }
</script>