<template>
  <v-container>
    <v-row align="center" justify="center">
      <v-col cols="12" md="12">
        <v-alert
          type="success"
          icon="mdi-bank-check"
          text
          prominent
          outlined
          v-if="this.reponse.result.prediction == 1"
        >
          {{ this.reponse.result.probaPercentile }} % Healthy company!
        </v-alert>
        <v-alert
          text
          outlined
          color="deep-orange"
          type="error"
          icon="mdi-bank-off-outline"
          prominent
          v-else
        >
          {{ this.reponse.result.probaPercentile }} % Risk of bankruptcy!
        </v-alert>
      </v-col>
    </v-row>
    <v-row justify="center" align="center">
      <v-col cols="12" md="4" align="center">
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
  name: "Result",
  props: {
    reponse: {
      type: Object,
      required: true,
    },
    risk: {
      type: Number,
      required: true,
    }
  },
  methods: {
    restart: function () {
      this.$emit("restart");
    },
  },
};
</script>

<style>
</style>