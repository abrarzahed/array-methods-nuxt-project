<template>
  <v-app>
    <v-app-bar app elevation="0">
      <v-container class="ml-7">
        <div class="d-flex align-center justify-space-between">
          <v-toolbar-title class="info--text"
            >Vuetify & Nuxtjs Project</v-toolbar-title
          >

          <v-icon large @click="$vuetify.theme.dark = !$vuetify.theme.dark">
            mdi-theme-light-dark
          </v-icon>
        </div>
      </v-container>

      <v-spacer />
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt class="my-5" />
      </v-container>
    </v-main>

    <v-footer class="footer">
      <span class="text--center"
        >&copy; {{ new Date().getFullYear() }} Zahed Abrar</span
      >
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: "DefaultLayout",
  data() {
    return {};
  },
};
</script>
<style>
.footer {
  text-align: center !important;
}
</style>
