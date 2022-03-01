<template>
  <v-container>
    <v-row align="center" justify="center">
      <v-col cols="12" md="3">
        <div v-if="this.reponse.result.prediction == 1">
          <v-icon x-large>mdi-bank-check</v-icon>
        </div>
        <div v-else>
          <v-icon x-large>mdi-bank-off-outline</v-icon>
        </div>
      </v-col>
      <v-col cols="12" md="3">
        <h1 class="display-4">{{ this.reponse.result.probaPercentile }} %</h1>
      </v-col>
    </v-row>
    <v-row justify="center">
       <v-col cols="12" md="3" >
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