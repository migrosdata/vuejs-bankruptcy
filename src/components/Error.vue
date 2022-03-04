<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <h1 class="display-2 font-weight-bold mb-3">Something went wrong</h1>
        {{this.error}}
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-col cols="12" md="3">
        <v-btn @click="restart">
          Nouvelle prédiction
          <v-icon large>mdi-piggy-bank</v-icon>
        </v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "Error",
  methods: {
    restart: function () {
      this.$emit("restart");
    },
  },
  props: {
    error: {
      type: Error,
      required: true,
    },
  },
};
</script>

<style>
</style>