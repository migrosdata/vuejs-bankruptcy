<template>
  <v-app>
    <v-main>
      <v-toolbar
        light
        src="https://cdn.vuetifyjs.com/images/backgrounds/vbanner.jpg"
      >
        <v-toolbar-title class="text-h3 white--text">Bankruptcy </v-toolbar-title>
        <v-img :src="require('@/assets/bankruptMan.png')" contain height="60" />
      </v-toolbar>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  components: {},

  data: () => ({
    //
  }),
};
</script>
