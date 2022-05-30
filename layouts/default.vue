<template>
  <v-app>
    <v-main>
      <nuxt />
    </v-main>
  </v-app>
</template>

<script>

export default {
  name: 'DefaultLayout',
  data () {
    return {
      title: 'mblfront',
    }
  }, 
}
</script>
<style>
a{
  text-decoration: none;
}
</style>
