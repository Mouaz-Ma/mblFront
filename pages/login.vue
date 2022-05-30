<template>
  <v-app>
    <logIn />
  </v-app>
</template>
<script>
    import logIn from "@/components/loginForm";
export default {
    auth: false,
    components: {logIn}
}
</script>