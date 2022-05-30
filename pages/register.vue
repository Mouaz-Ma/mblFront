<template>
  <v-app>
    <register />
  </v-app>
</template>
<script>
  import register from "@/components/registerForm";
  export default {
    auth: false,
    components: {register}
  }
</script>